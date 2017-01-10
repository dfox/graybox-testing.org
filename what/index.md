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

Testing is one of those development practices which for some reason
gets contentious. Almost all developers believe that testing is a good
idea, but not all of us agree on which testing strategies are the most
effective. Rather than try to push a particular strategy as *best*,
we'll focus on which kinds of tests we should have in an application
at *minimum*, leaving the rest up for discussion. Before we talk about
gray box testing, though, well need to discuss the far ends of the
spectrum.

## Black Box Testing

In [black box testing](https://en.wikipedia.org/wiki/Black-box_testing), the
application is tested "from outside", without any knowledge of how the
system functions internally. This is often done via the user
interface. Black box testing does not need to be automated. In fact
even if it can be automated, it's often advisable to test manually as
well.  Automated tests are good at verifying functionality, but they
can't tell if a user interface element is misaligned or a button can't
be pressed because of a
[z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
bug. In order to know what to test, a tester will consult a
specification, which outlines how a feature should perform and what
the expected inputs and outputs are. 

## White Box Testing

[White box testing](https://en.wikipedia.org/wiki/White-box_testing)
is more concerned about the internals of an application, including its
data structures, algorithms, and the paths the code takes during
operation. In order to write these kinds of tests, a developer must
have intimate knowledge of the application source code. These kinds of
tests tend to be very brittle, as they are highly coupled to the code
itself. 

## Gray Box Testing

[Gray box](https://en.wikipedia.org/wiki/Gray_box_testing) is a hybrid
of both white and black box testing. Tests are driven by the user
interface, but also have some knowledge of, and validate system
internals. How much of each style is used can vary, but we recommend
approaching it in a way the minimizes how much knowledge the tests
have of the system.