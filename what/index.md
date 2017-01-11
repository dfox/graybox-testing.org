---
layout: article
title: "What is Gray Box Testing?"
date: 2017-01-10T09:44:20-04:00
modified: 2014-08-27T14:56:44-04:00
excerpt: "Grey box testing is somewhere between white box and black box testing. Tests are driven by the user interface, but have some knowledge about system internals."
image:
  feature:
  teaser:
  thumb:
share: false
ads: false
---

Testing is one of those software development practices which for some
reason
[gets contentious](https://martinfowler.com/articles/is-tdd-dead/).
Almost all developers believe that testing is a good idea, but not all
agree on which testing strategy is the most effective. Rather than
try to push a particular strategy as *best*, we'll focus on a kind of
test we feel an application should have at a bare *minimum*: a
functional, or behavioral test. We believe that a specific style of
gray box testing is the most minimal, yet thorough, type of functional
test. Before we talk about gray box testing, we'll need to discuss
the far ends of the spectrum: black box and white box testing.

## Black Box Testing

In [black box testing](https://en.wikipedia.org/wiki/Black-box_testing), the
application is tested "from outside", without any knowledge of how the
system functions internally. This is often done via the user
interface. Black box testing does not need to be automated. In fact
even if it can be automated, it's often advisable to test manually as
well.  Automated tests are good at verifying functionality, but can't
tell if a user interface element is misaligned or a button can't be
pressed because of a
[z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
bug. Until we have solutions for those issues, those kinds of
assertions are best left up to humans.

In order to know what to test, a test writer will consult a
specification, which outlines how a feature should perform and what
the expected inputs and outputs are. There are many ways to write a
specification, but we have a simple format that is easy to read and
understand, and can be used for a number of different purposes.  We'll
cover that in the [next section](/specifications/).

## White Box Testing

[White box testing](https://en.wikipedia.org/wiki/White-box_testing)
is more concerned about the internals of an application, including its
data structures, algorithms, and the paths the code takes during
operation. In order to write these kinds of tests, a developer must
have intimate knowledge of the application source code. These kinds of
tests tend to be very brittle, as they are highly coupled to the code
itself. Though white box tests may be able to ensure all code paths
function properly, they tend to miss areas which lack sufficient
specification. Depending on what level they test at, they can also
miss issues which arise when modules are fully integrated together.

## Gray Box Testing

[Gray box](https://en.wikipedia.org/wiki/Gray_box_testing) is a hybrid
of both white and black box testing. Tests are driven by the user
interface, but also have some knowledge of system internals. That
knowledge is used to validate the changes to the system which would
not otherwise be visible to a black box style test. However, that
knowledge is limited in scope to only the changes to the state of the
application. 

