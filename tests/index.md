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

Once a functional specification is written, it can be used to write an
automated test. The test will be written to automate the steps in the
specification exactly as the user would perform them in the user
interface. The preconditions and side effect assertions are set up and
tested using the same language and platform the application is written
in.

The libraries for user interface testing on mobile devices are
unfortunately not as mature as what is available for web
applications. When mature solutions exist for iOS and Android, they
will be added here.

## Web Applications

The most mature testing tool for web applications is
[Selenium](http://docs.seleniumhq.org). These days, front-end
developers are very fluent in
[Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
and [NodeJS](https://nodejs.org), and since they are the ones who will
be creating the user interface, they should be the ones writing the
user interface tests. There is a fantastic, NodeJS-based frontend for
Selenium called [Nightwatch](http://nightwatchjs.org) which provides a
fluent, Javascript-based interface. This makes it very easy to convert
a functional specification into an automated test.

