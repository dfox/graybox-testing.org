---
layout: article
title: "How to Write Tests"
date: 2017-01-07T09:44:20-04:00
modified: 2017-01-10T09:44:20-04:00
excerpt: "Once you have specifications, they are easy to turn into user inteface tests"
image:
  feature:
  teaser:
  thumb:
share: false
ads: false
---

Once a [functional specification](/specifications/) is written, it can
be used to write an automated test. The test will perform the steps in
the specification exactly as the user would perform them in the user
interface. The preconditions and side effect assertions are set up and
tested using the same language and platform the application is written
in, and are called remotely from the user interface test.

\* The libraries for user interface testing on mobile devices are
unfortunately not as mature as what is available for web
applications. When mature solutions exist for iOS and Android, they
will be added here.

## Web Applications

The most mature test automation tool for web applications is
[Selenium](http://docs.seleniumhq.org). These days, front-end
developers are very fluent in
[Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
and [Node.js](https://nodejs.org), and since they are the ones who will
be creating the user interface, they should be the ones writing the
user interface tests. There is a Node.js-based frontend for Selenium
called [Nightwatch](http://nightwatchjs.org) which provides a fluent,
Javascript-based interface. This makes it very easy to convert a
functional specification into an automated test.

The Nightwatch test can automate the browser interaction, but the
backend of the application may not expose an API which allows it to
assert the side effects it performs. It also may not be written in
Javascript, but could be on any number of other platforms. For
example, [Java](https://java.com). In order for the frontend to make
those assertions, a separate test server is run along side the web
application's server. It exposes a
[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
API over
[HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
which allows the user interface test to run setup routines and tests
on the backend, and provides test data which can be used to coordinate
between the front and back end tests. By using a standard REST
HTTP-based protocol, any frontend can assert side effects on any
backend, regardless of platform. This allows applications which have
multiple front ends and/or multiple backends to reuse tests on either.

### Example

For this example, the Nightwatch frontend will access the
[JUnit HTTP](https://github.com/dfox/junit-http) backend using the
[nightwatch-js-remote-assert](https://github.com/dfox/nightwatch-js-remote-assert)
plugins. These are available in the [tools](/tools/) section of the
site. It will reference the [example specification](/specifications/)
in the previous section.

#### Agree on Test Data

At this point, if the frontend and backend developers are different
people, there must be some agreement on how to coordinate the test
data that will be used. Because the backend test will need to assert
the presence of a note on the server, and test that its name and
content are correct, it makes sense to have those available to both
tests. Test data is simply a set of [JSON](http://json.org) files
which are exposed by the test backend and are available in the
Nightwatch test via a simple function call.

For this test, we need to coordinate both the name and note content
between the front and backend, so the test data, saved in a file
called **notes.json**, looks like this:

```json
{
    "save": {
        "name": "save-note",
        "contents": "This is my saved note"
    }
}

```

#### Agree on Test Naming

The frontend and backend developers will also need to agree on the
name of the test group and the name of the test to be performed on the
backend so Nightwatch can call it. The JUnit HTTP backend exposes the
canonical name of the test class as the test group. So the test group
will be **io.dfox.junit.http.example.ExampleTest**. The name of the test
will be **noteSaved**.

#### Write Frontend Test

Now both developers can start writing their tests. The Nightwatch test
looks like this:

```javascript
module.exports = {
  'Notes can be saved' : browser => {
    browser.loadTestData('notes.json', notes => {
      browser
        .url('http://localhost/notes')
        .waitForElementVisible('body', 1000)
        .setValue('input[id=note-name]', notes.save.name)
        .setValue('textarea[id=note-content]', notes.save.contents)
        .click('button[id=save-button]')
        .pause(1000)
        .assert.containsText('#status', 'Saved note: ' + notes.save.name)
        .assert.remote('io.dfox.junit.http.example.ExampleTest', 'noteSaved')
        .end();
    });
  }
}
```

The test data is loaded first by calling the **loadTestData()**
function with the name of the test data file, in this case,
**notes.json**. The plugin takes care of calling the backend and makes
the data available to the test executed via its callback. Next comes
the Nightwatch code which duplicates the steps in the
specification. You can see how the test data is referenced in the
test.

#### Write Backend Test

Near the end of the Nightwatch test, the backend test is executed by
calling the **assert.remote()** function with the test group and name
the developers agreed to before. This makes an HTTP call to the
backend which runs the test and reports its results to the plugin. The
java test looks like this:

```java
package io.dfox.junit.http.example;

import org.apache.commons.io.IOUtils;
import static io.dfox.junit.http.util.TestUtils.getTestData;
import static org.junit.Assert.assertEquals;
import com.fasterxml.jackson.databind.JsonNode;
import java.io.IOException;
import java.io.InputStream;
import org.junit.Test;

...

public class ExampleTest {

    private static NoteRepository repository;

    @BeforeClass
    public static void setUp() throws IOException {
        final File tempDir = new File(System.getProperty("java.io.tmpdir"),
                                      NoteRepository.class.getName());
        repository = new NoteRepository(tempDir);
        repository.init();
    }

    ...

    @Test
    public void noteSaved() throws IOException {
        JsonNode notesFixture = getTestData("notes.json");
        JsonNode noteFixture = notesFixture.path("save");
        String name = noteFixture.path("name").asText();
        String expectedContents = noteFixture.path("contents").asText();

        Optional<InputStream> note = repository.getNote(name);
        assertTrue(note.isPresent());
        try(InputStream stream = note.get()){
            String contents = IOUtils.toString(stream);
            assertEquals(expectedContents, contents);
        }
    }
```

Note how the test data is reused in the Java test by calling
**getTestData()**. This makes the tests less brittle, as the
information is only specified in one place. Also, the data access
adapter, referenced here as **repository**, is used to get the note to
assert its name and contents. This makes the backend test independent
of that implementation, and also allows that code to be reused rather
than duplicated in the test.

If the Java test is successful, the Nightwatch test will
pass. Otherwise, a stacktrace will be sent back to Nightwatch so it
will be saved in the test log for debugging purposes.



