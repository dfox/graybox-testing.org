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

Testing is one of those development practices which for some reason is
very contentious. Almost all developers believe that testing is a good
idea, but not all of us agree on which testing strategies are the
best. Rather than try to push a particular strategy as *best*, we'll
focus on which kinds of tests we should have in an application at
*minimum*, leaving the rest up for discussion. 

## Black Box Testing

In [black box testing](https://en.wikipedia.org/wiki/Black-box_testing), the
application is tested "from outside", without any knowledge of how the
system functions internally. In order to know what to test, a tester
will consult a specification, which outlines how a feature should
perform and what the expected inputs and outputs are. Depending on the
design of the application, blackbox testing can

## White Box Testing

[White box testing](https://en.wikipedia.org/wiki/White-box_testing)
is more concerned about the internals of an application, including its
data structures, algorithms, and the paths the code takes during
operation. In order to write these kinds of tests, a developer must
have intimate knowledge of the application source code.

## Gray Box Testing

[Gray box](https://en.wikipedia.org/wiki/Gray_box_testing) is a hybrid
of both white and blackbox testing. Tests are driven by the user
interface, but also have some knowledge of, and validate system
internals. How much of each style is used can vary, but we recommend
approaching it in a way the minimizes how much knowledge the tests
have of the system.