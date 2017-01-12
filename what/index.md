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

Testing is one of those software development practices that there are
a lot of [opinions](https://martinfowler.com/articles/is-tdd-dead/)
about. Almost all developers believe that testing is important, but
not all agree on which testing strategy is the most effective.

Rather than try to push a particular strategy as *best*, this site
focuses on a kind of test an application should have at a bare
*minimum*: a functional test. This kind of test validates the steps a
user takes in an application to perform a task and how those steps
affect the state of the application. It is not a replacement for other
types of testing that a developer might do during the course of
development, such as unit testing. Those are still valuable. However,
as the number of tests increase, there tends to be diminishing
returns. The cost of complete test coverage at every layer of the
application may be justified for software which runs an insulin pump,
but a non-critical business application probably doesn't have the same
requirements. Yet both applications need to be tested to ensure they
work as intended, so there should be a minimal set of tests which can
validate that functionality.

The specific style of gray box testing described on this site is the
most minimal, yet thorough, type of functional test. Before we go into
details, we'll need to discuss the strategies at the far ends of the
spectrum: black box and white box testing.

## Black Box Testing

In
[black box testing](https://en.wikipedia.org/wiki/Black-box_testing),
the application is tested "from outside", without any knowledge of how
the system functions internally. This is often done via the user
interface, but could also be at a deeper layer of an application. For
the purposes of this site, we'll focus on user interface testing.

A black box test validates a series of steps that a user performs in
an application and that the user interface responds as intended. It
does not have knowledge of, and therefore cannot validate, the
internal state of the application, other than what can be inferred
from the user interface itself.

With modern [tools](/tools/), these kinds of tests can be
automated. This significantly decreases the cost of running the tests
regularly. However, even if they are automated, it's important to test
manually as well. Automated tests can verify functionality, but can't
tell if a user interface element is misaligned or a button can't be
pressed because of a
[z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
bug. Therefore it's important to have a way to share a test between
both humans and computers. That way automated tests can be run
regularly, while the human tests can be run at critical junctures,
such as before a release.

A specification provides the basis for an automated test as well as
functioning as a script for human quality assurance. There are many
ways to write a specification, but we have a simple format that is
easy to read and understand, and can be used for both purposes. We'll
cover that in the [next section](/specifications/).

## White Box Testing

[White box testing](https://en.wikipedia.org/wiki/White-box_testing)
is more concerned about the internals of an application, including its
data structures, algorithms, and the paths the code takes during
operation. In order to write these kinds of tests, a developer must
have intimate knowledge of the application source code and the
different systems involved. They tend to be more brittle, as they are
tightly coupled to the code itself. However, in order to really
validate that an application functions as intended, the tests need
*some* knowledge of its internals. They key is to minimize that
knowledge and write the tests in such a way that changes to the tests
are minimized as the source code changes.

## Gray Box Testing

[Gray box testing](https://en.wikipedia.org/wiki/Gray_box_testing) is
a hybrid of both white box and black box testing. Tests perform the
steps of an interaction "from the outside", but also validate the
changes that occur to the application's state "on the inside".

In the type of gray box test promoted here, the test has access to the
modules in an application which perform the side effects and have
access to its data. One common way to do this is by using an
architectural pattern called
[ports and adapters](http://alistair.cockburn.us/Hexagonal+architecture)
(otherwise known as hexagonal). In this pattern, there is an
application core surrounded by a set of adapters. The application core
contains the pure business logic, while the adapters each serve a
specific *purpose*, generally to perform side effects. A thin *service
layer* coordinates how the adapters and core interact. This allows
different *technologies* to be plugged into the application to serve
those different purposes. With this architecure, tests can reuse the
adapters to perform validation of the side effects which occur in an
interaction. This is generally what a black box test lacks.

In order for the tests to have access to the adapters, it's important
to modularize the codebase and keep each type of technology in a
separate module. For example, if the application has a set of adapters
for data access, and those are implemented in DatabaseXYZ, there
should be a DatabaseXYZ-specific module containing those
implementations. Then, in order to validate that data access was
performed correctly, a test can simply import that module and use its
API to perform the validation. This has the advantage that if a new
adapter is written, the test need not be updated. It can simply import
the new adapter implementation and the test should still pass. By
using
[dependency injection](https://en.wikipedia.org/wiki/Dependency_injection),
this can even be done simply by configuration.

In order to ensure the adapters function correctly, the developer must
write white box tests for each of their API functions. In the data
access example above, the test should ensure that when the function is
called with a specific input, that the database table(s) are updated
correctly. 






