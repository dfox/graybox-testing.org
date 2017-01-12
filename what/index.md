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
Almost all developers believe that testing is important, but not all
agree on which testing strategy is the most effective.

Rather than try to push a particular strategy as *best*, we'll focus
on a kind of test we feel an application should have at a bare
*minimum*: a functional test. This kind of test validates the steps a
user takes in an application to perform a task and how those steps
affect the state of the application. It is not a replacement for other
types of testing that a developer might do during the course of
development, such as unit testing. Those are still valuable. However,
as the number of tests increase, there tends to be diminishing
returns. The cost of complete test coverage at every layer of the
application may be justified for software which runs an insulin
pump. However, a non-critical business application probably doesn't
have the same requirements. Both applications need to be tested to
ensure they work as intended, so there must be a minimal set of tests
we can use to validate that functionality.

We believe that a specific style of gray box testing is the most
minimal, yet thorough, type of functional test. Before we go into
details, we'll need to discuss the far ends of the spectrum: black box
and white box testing.

## Black Box Testing

In
[black box testing](https://en.wikipedia.org/wiki/Black-box_testing),
the application is tested "from outside", without any knowledge of how
the system functions internally. This is often done via the user
interface, but could also be a unit test at a deeper layer of an
application. For the purposes of this site, we'll focus on user
interface testing.

A black box test validates that given a series of steps that a user
performs in an application, that the user interface responds as
intended. It does not have knowledge of, and therefore cannot
validate, the internal state of the application, other than can be
inferred from the user interface itself. 

With modern tools, these kinds of tests can be automated. This
significantly decreases the cost of running the tests
regularly. However, even if they can be automated, it's often
advisable to test manually as well.  Automated tests can verify
functionality, but can't tell if a user interface element is
misaligned or a button can't be pressed because of a
[z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)
bug. Therefore it's important to have a way to share a test between
both humans and computers. That way automated tests can be run
regularly, while the human tests can be run at critical junctures,
such as before a release.

A specification provides the basis for an automated test as well as
being a script for human quality assurance. There are many ways to
write a specification, but we have a simple format that is easy to
read and understand, and can be used for both purposes. We'll cover
that in the [next section](/specifications/).

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
not otherwise be visible to a black box test. However, that knowledge
is limited in scope to only the changes to the state of the
application.

In the type of gray box test we promote, the test has access to the
modules in an application which perform the side effects. 

