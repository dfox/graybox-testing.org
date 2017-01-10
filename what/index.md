---
layout: article
title: "What is Graybox Testing?"
date: 2017-01-10T09:44:20-04:00
modified: 2014-08-27T14:56:44-04:00
excerpt: "Greybox testing is somewhere between whitebox and blackbox testing. Tests are driven by the user interface, but have some knowledge about system internals."
image:
  feature:
  teaser:
  thumb:
share: false
ads: false
---

[Greybox](https://en.wikipedia.org/wiki/Gray_box_testing) testing is
a hybrid of
[whitebox](https://en.wikipedia.org/wiki/White-box_testing) and
[blackbox](https://en.wikipedia.org/wiki/Black-box_testing)
testing. Tests are driven by the user interface, but the have some
knowledge about system internals. To understand it fully, we'll talk
about both whitebox and blackbox testing, what their strengths and
weaknesses are, and how a hybrid of the two, graybox, can give us the
best of both worlds.

## Blackbox Testing

In blackbox testing, the application is tested "from outside", without
any knowledge of how the system functions internally. In order to know
what to test, a tester will consult a specification, which outlines
how a feature should perform and what the expected inputs and outputs
are. Depending on the design of the application, blackbox testing can 

## Whitebox Testing

Whitebox testing is more concerned about the internals of an
application, including its data structures, algorithms, and the paths
the code takes during operation. In order to write these kinds of
tests, a developer must have intimate knowledge of the application
source code.

## Graybox Testing

Graybox is a some combination of both white and blackbox testing. How
much of each style is used can vary, but we recommend approaching it
in a way the minimizes how much knowledge the tests have of the
system. 