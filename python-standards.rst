Python Coding Standards and Recommendations
===========================================

By and large, we utilizing available tools
to help format and lint the code
to keep it consistent and readable.
Outside of what those tools can provide,
we do have some suggested guidelines as well.

Code should be written not only to be executed by a machine
but also to be read and maintained.
Thus, the purpose of coding standards
is not to impede the development process of individual developers,
but to help ensure that the code meets a minimum standard of readability.

Coding Standards
----------------

Some standards that cannot be easily handled by available tooling and linters:

* Names should be descriptive. Follow the DAMP_ principle.
  With the exception of loops, generator expressions, and comprehensions,
  there should never be single letter variable/class/etc names in the code.
* Comment code sections that are
  not readily apparent in their purpose.
* Keep methods small and atomic.
* Keep object oriented principles in mind
  (inheritance, encapsulation, etc.).
* Delete dead code.
  We are using version control
  that lets us go back and retrieve it if needed.
* Don't add speculative
  or "will need this soon" code.
  Such code should be added
  along with the code that will use it,
  otherwise it is just dead code.
* Abstract code where possible.
* Look for patterns
  and create a generic method.
* Use external mechanisms for setting parameters
  (config files, databases, etc.).
* Don't hard-code test data.
* Follow the DRY_ principle.
* Raise exceptions,
  don't return error code values.

.. _`DAMP`: https://medium.com/mutual-of-omaha-digital-experience-and-design-team/damp-programming-reviving-readability-d84647cc5b2e
.. _`DRY`: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
