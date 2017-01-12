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

In order to know what to test, there must first be a description of
what the application is supposed to do. The easiest way to do that is
with a functional specification that describes each feature. In order
for the specification to be useful as a basis for an automated test
and as a script for a human quality assurance person, we've chosen a
simple format that serves both purposes.

## Design by Contract

A
[design by contract](https://en.wikipedia.org/wiki/Design_by_contract)
specification outlines the steps a user performs in the application
for a single interaction and how the interaction affects the
application's state. In one variation, an interaction with an
application has the following properties:

* **Pre-conditions:** The state of the application before the interaction
* **Input:** The information transferred into the application from the interaction
* **Side-effect(s):** One or more side effects which occur
* **Output:** The output from the application in response to the input
* **Post-conditions:** The state of the application after the interaction

This allows a feature to be described in clear, concrete terms in the
simplest way possible.

## Example

The following example, which is included with [the tools](/tools/)
available on this site, shows how design by contract can be realized
in a simple format. It is for a simple note taking application:

#### Pre-conditions
* A note with the name "my-note" does not exist

#### Steps
* Browse to URL http://localhost/notes
* Set the name of the note to "my-note"
* Set the contents of the note to "This is my note"
* Click "Save"
* Assert that the status message changes to "Saved note: my-note"

#### Post-conditions
* A note with the name "my-note" exists and contains the content "This
  is my note"

The specification is very simple and lightweight, and contains enough
information to both implement the functionality and write a test for
it. There will be other artifacts needed to implement a feature like
this, for example designs for the user interface, but this format
provides the minimal information.




