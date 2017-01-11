---
layout: article
title: "How to Write Specifications"
date: 2017-01-07T09:44:20-04:00
modified: 2017-01-07T14:56:44-04:00
excerpt: "To start testing, you first need to write functional specifications"
image:
  feature:
  teaser:
  thumb:
share: false
ads: false
---

In order to know what to test, you first need to know what the
application is supposed to do. The easiest way to do that is to write
a minimal functional specification for each feature.

## Design by Contract

We prefer a type of functional specification commonly known as
[design by contract](https://en.wikipedia.org/wiki/Design_by_contract).
The specification outlines the steps a user performs in the
application for a single interaction and how the interaction affects
the application's state. We can think about an interaction with an
application having the following properties:

* **Pre-conditions:** The state of the application before the interaction
* **Input:** The information transferred into the application from the interaction
* **Side-effect(s):** One or more side effects which occur
* **Output:** The output from the application in response to the input
* **Post-conditions:** The state of the application after the interaction

Thinking about these properties of an interaction, we can specify the
interaction with a simple format that captures the information we need
in a format that matches well with how tests are written.

## Example

Here's an example specification for one of the example programs
included with our tools:

#### Pre-conditions
* A note with the name "my-note" does not exist

#### Steps
* Browse to URL http://localhost:8082
* Set the name of the note to "my-note"
* Set the contents of the note to "This is my note"
* Click "Save"
* Assert that the status says "Saved note: my-note"

#### Post-conditions
* A note with the name "my-note" exists and contains the content "This
  is my note"
