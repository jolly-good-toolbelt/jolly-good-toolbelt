Gherkin
=======

Gherkin_ is our preferred mechanism for documenting requirements.
It is stored in `.feature` files
which are both human readable,
and test-tool runnable.
While Gherkin can be used
as executable requirements/tests with a variety of tools,
it is, itself, programming language agnostic.

This document describes our recommendations and best practices
to be applied above and beyond the bare minimum for valid Gherkin.

Gherkin Feature File Coding Standard
------------------------------------

* The maximum recommend line width is 100 characters.
* Step keywords are left-aligned.
* Indentation is a multiple of two spaces.
* Blank Lines

  * Scenarios are separated by a single blank line.
  * No blank lines between a summary line and the following description.
    The description is indented two spaces from the summary line.
  * Example tables have a blank line before them.
  * Backgrounds have a blank line before them.
  * Data tables follow their particular step definition with no blank lines.
  * No blank lines at the end of the file.
  * The last line of the file will have a newline at the end
    (just as with code).

* Comments must appear on lines by themselves.
* Meet current standards when adding new Gherkin to existing files

  * When adding a new scenario or step to an existing Gherkin file,
    the new Gherkin will meet the current code standards
    even if this is inconsistent with the existing file.
  * When reusing an existing Gherkin step
    that doesn't meet current code standards,
    modify the step to also accept a new Gherkin line
    that does meet current code standards,
    and use that Gherkin for new code.
    It is out of scope for the PR to change other places
    where the outdated Gherkin is used.

* Avoid the `Cucumber Anti-Patterns`_

  * Note that for UI testing,
    Scenario Outlines are more common than the Anti-Patterns would suggest,
    because the interface itself is that complicated.

* Gherkin Language

  * Avoid using the word `"should"`_ in steps::

     # Bad
     Then the search results should include the triggered event

     # Good
     Then the search results include the triggered event

  * Be specific::

     # Bad
     When the system is ready

     # Good
     When the login screen is visible

  * Write in the active voice::

     # Bad
     When an event is submitted

     # Good
     When the user submits an event

  * Favor the present tense::

     # Bad
     Then the nested event(s) will complete before the parents

     # Good
     Then the nested event(s) complete before the parents

  * Use third person over first person::

     # Bad
     When I click the login button

     # Good
     When the user clicks the login button

  * Do not describe the action being taken (e.g., do not say "Verify that...")::

     # Bad
     Then verify the executed event status is BAKING

     # Good
     Then the executed event status is BAKING

  * It is better to have clearer steps than reused steps.

  * **Then** steps will avoid pronouns; **Then** steps are just for checking
    the results from a **When** step, no subject is needed::

     # Bad
     Then the user is redirected to the login page

     # Good
     Then the system displays the login page

  * Follow `Good Gherkin Scenario Titles`_

.. _`Gherkin`: https://github.com/cucumber/cucumber/wiki/Gherkin
.. _`Cucumber Anti-Patterns`: https://cucumber.io/blog/2016/07/01/cucumber-antipatterns-part-one
.. _`"should"`: https://jml.io/pages/test-docstrings.html
.. _`Good Gherkin Scenario Titles`: https://automationpanda.com/2018/01/31/good-gherkin-scenario-titles/
