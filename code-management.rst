Code Management
===============

We maintain a public repository with a single master branch.
Each developer should create an account-level fork of that repository
and clone that fork locally for development.

Developers should submit changes via Pull Request for review and integration.
For more information on why we use Forks and Pull Requests instead of branches,
please see `Git Branches Considered Harmful`_.

.. note::
   To prevent accidentally pushing to the upstream repository,
   update the update push URL to a non-valid URL.
   We recommend using DISABLE as a visual indicator::

        git remote set-url --push upstream DISABLE

Repository Conventions
----------------------

* Each repository should have available:

  * ``README.md`` or ``README.rst`` explaining what it is,
    who the audience is, etc.
    If applicable,
    this can simply be a link
    to the documentation built from a documentation tool.

  * ``env-setup`` a callable that sets up the environment:

    * to be run by humans at will
    * to be run (indirectly) via automation tooling
      (such as Jenkins or Travis CI)
    * will fail if it is not running in a virtual environment (if appropriate)
    * otherwise will install
      and configure the environment for testing

  * ``self-check`` a callable that does a self-check on the repository:

    * to be run by humans at will (such as before pull requests)
    * to be run by automation tooling for pull request acceptance testing.
    * This callable should support a --setup command line parameter
      which will invoke the env-setup script
      to make sure the environment is good
      before running self-check logic.
    * automation tooling must always pass the --setup parameter
      to ensure the environment is up to date.

  * ``run-tests`` a callable that handles the boilerplate of running tests:

    * to be run by humans at will
    * to be run by automation tooling for regular runs of test jobs
    * this script should support a --check command line parameter
      which will invoke the self-check script with the --setup option
      to make sure the environment is good
      and the self-checks all pass

  * ``build-docs`` a callable that handles building the repository
    documentation:

    * to be run by humans at will
    * to be run by automation tooling for pull request merges

.. note::
   For the callables,
   use the appropriate language
   and extension for your environment.
   The `jgt_tools`_ library provides all the callables
   for any Python-based project.


General Code Management Policies
--------------------------------

Commit Management
~~~~~~~~~~~~~~~~~

Commits should be smaller, related commits
rather than large and monolithic.
Do not lump together unrelated code into a single commit,
unless requested to squash a pull request by a reviewer.

Commit Messages
~~~~~~~~~~~~~~~

When doing a commit,
we encourage following the format described in
`A Note About Git Commit Messages`_.

It is recommended,
although not required,
to utilize the prefixes found in `Pull Requests`_.

.. note::
   If the pull request has only one commit,
   GitHub uses the commit message to try and pre-populate the title and comment.
   By following the suggested format above,
   the pull request title
   and comment should need minimal changes.
   If the prefix is used,
   the pull request title will have it
   which is where the prefix **is** required.

Pull Requests
~~~~~~~~~~~~~

Each pull request must have a title and a comment.
These should conform to the standards
described in `Commit Messages`_ with one addition:
the title must be in the format of
``<Prefix>: <Title>`` where ``<Prefix>`` is one of the following:

============  ===============================================================
Prefix        | Use Case
============  ===============================================================
<Ticket_ID>   | Any commit related to a specific ticket
Enhancement   | Any enhancement outside of a ticket (should be small changes)
Fix           | Any fix outside of a ticket (should be small changes)
FF            | A fast follow for a previous pull request (usually small very
              | specific changes, expected to be completed quickly after the
              | pull request merges)
Spike         | A proof-of-concept that may not be merged as-is;
              | can include a ticket ID
============  ===============================================================

A pull request should contain a single unit of work.
The pull request should only add, remove, or change
one feature / group of features.
Do not bundle features together.
Changes that need to be made
across multiple repositories are acceptable,
but reference the partnering pull requests within each other.
To quote the `Linux kernel submission guidelines`_:

    For example, if your changes include both bug fixes
    and performance enhancements for a single driver,
    separate those changes into two or more patches.
    If your changes include an API update,
    and a new driver which uses that new API,
    separate those into two pull requests.

    On the other hand,
    if you make a single change to numerous files,
    group those changes into a single pull request.
    Thus a single logical change
    is contained within a single pull request.

    The point to remember is
    that each pull request should make
    an easily understood change
    that can be verified by reviewers.
    Each pull request should be justifiable
    on its own merits.

The final step before creating a pull request
is to assign the appropriate reviewers.
See `Collaborate / Review`_ to help determine
the appropriate first reviewer(s).

Collaborate / Review
~~~~~~~~~~~~~~~~~~~~

Any pull request submission needs to be reviewed
by at one least two people.
The final reviewer is responsible
for merging the pull request.

Once a pull request is ready,
assign all eligible members for review.
This can be tweaked if there is a previous arrangement,
such as when a particular individual is invested in the changes being made
or a small group has worked heavily in one area.
In that case, the assignment may be more focused.

All Participants
++++++++++++++++

Try to keep all discussion contained within the pull request.
If a discussion occurs outside of the pull request comments
(e.g., video chat),
a summary of the discussion should be added
as a comment by the current assignee.

Once the pull request has been submitted,
each iteration should be completed
within one business day.
If more time is needed,
please post a comment informing all participants.

.. admonition:: Treat Others Like Friends and Family
   :class: note

   It is always a good reminder
   that during a pull request code review,
   it is the code being reviewed,
   not the coder.
   When leaving a comment as a part of a pull request,
   ensure that the comments address the code
   and not the coder.
   When reading a comment,
   remember that the pull review process is intended
   as a mechanism for improving the code base
   and is a mechanism for facilitating that improvement
   rather than speaking negatively about an individual or their abilities.

Participating As a Reviewer
+++++++++++++++++++++++++++

When starting to review a pull request,
please remove any other reviewers.

If approving the pull request,
and you are not the final reviewer,
assign it to everyone who has not yet reviewed.
if the final reviewer,
merge the pull request.

If requesting changes,
assign the pull request back to the original author.

If providing comments,
you can either assign back to the original author for respone,
or assign it to everyone who has not yet reviewed
so that the review process may continue to flow.

Participating As an Author
++++++++++++++++++++++++++

When participating as an author for a code review,
if any comments are added or changes are requested,
make the necessary changes,
answer any questions,
and assign the pull request back to
the individual requesting the changes.

.. _`jgt_tools`: https://pypi.org/project/jgt-tools/
.. _`Git Branches Considered Harmful`: http://hintjens.com/blog:24
.. _`A Note About Git Commit Messages`: https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
.. _`Linux kernel submission guidelines`: https://www.kernel.org/doc/Documentation/SubmittingPatches
