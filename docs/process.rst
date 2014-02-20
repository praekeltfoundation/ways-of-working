Intellectual Property
=====================

**All** code produced in exchange for remuneration by a Praekelt company must
have copyright assigned to "Praekelt Foundation" or "Praekelt Consulting"
as appropriate.

All code published into open Github repositories must be licenced under the
`BSD 3-Clause Licence`_. Any third party open source modules used for the project
must be under an explicit, compatible licence, and if belonging to you as
a development partner, must exist prior to the start of the project to
remain your IP.

Code snippets used from other sources (i.e. not complete files, or single files
lifted from other projects) must be attributed in the header of the file in a
comment, including URL of the source, and author.

Our project process
===================

The lifecycle of our projects is typically as follows:

1. We produce a Scope of Work for a project, which might not have all the
   technical details, but should be comprehensive enough to list all the
   features so that you can quote on the project's development. Wireframes
   may also be provided as part of the scope for your CE (Cost Estimate).
2. We work on a fixed cost basis for a fixed scope. If the scope changes,
   we ask you for a costing for the delta or new work.
3. The authorisation to proceed with work consists of a Purchase Order,
   without which you cannot invoice us - so never start work without the PO.
4. Development commences - see below. **If you don't have a github repo by this
   point, please bug us until we provide it - please do not use your own
   repo.**
5. We provide you with one QA server, with the same OS setup that we'll use
   in production - for all the projects you do for us, unless a project has
   special needs which justify its own QA server. **Please bug us for a
   QA URL for this project to be pointed to your QA server.** It must be on
   our domain for client UAT.
   Please note that QA may need sample or real data to be populated. Often,
   the QA data gets migrated to the production site when finally deploying
   that, so please ensure that dummy data can be cleaned up, and use
   **CMS credentials** on QA that are *suitable for production*.
6. You are responsible for deploying your code to this QA server, so that you
   can support the fixing of bugs found during our QA testing. You should
   **always** deploy to QA from the github repo, to avoid any side effects of
   uncommitted code.
7. We'll deploy to production so that we can support it - see below.

Our development process
=======================

The process involved in how we work is fairly straight forward and we
expect you to follow this as well.

1. We use `Git Flow`_'s convention with regard to branch names.
2. All work requires a ticket with a unique number or name.
3. Work happens in a `feature branch`_. Feature branches names are composed
   of the ticket / issue number along with a one-line description of the issue.
4. Write tests for the new features you are developing.
5. Make one change per commit, and follow `What's in a Good Commit?`_
6. Put the ticket number in the commit message. For github issues in particular,
   see `Closing issues via commit messages`_
7. Your schema changes are expected to be handled by a schema migration script.
8. When work in a feature branch is ready for review then we create a
   pull-request.
9. All collaborators on the GitHub repository are notified of the pull-request
   and will start the process of reviewing the changes.
10. Any issues, concerns or changes raised or recommended are expected to be
    attended to. Once done please notify the reviewers of the changes and
    ask for the changes to be re-reviewed.
11. Once all the changes are approved and one or more of the collaborators
    has left a `:+1:` in the pull-request's comments it can be merged into
    the main branch and is ready for a deploy.

For your code to be ready for review we have the following expectations:

1. It is to be pep8_ compliant and pyflakes_ is not raising any issues.
2. It is to have tests. Unless otherwise agreed, 90% test coverage is required. See Coverage_
3. The tests have to pass.
4. There are no commented lines of code.
5. There is adequate amount of documentation.

Example flow
~~~~~~~~~~~~

::

    $ virtualenv ve
    $ source ve/bin/activate
    (ve)$ git flow feature start issue-1-update-documentation
    (ve)$ git flow feature publish issue-1-update-documentation
    ..// hack hack hack // ..
    (ve)$ nosetests
    .............
    ----------------------------------------------------------------------
    Ran 13 tests in 0.194s
    OK
    (ve)$ git push
    (ve)$ hub pull-request -b develop -i 1
    https://github.com/praekelt/some-repository/pulls/1
    ..// review, update, re-eview, update, re-review ... +1 // ..
    (ve)$ git flow feature finish issue-1-update-documentation
    ..// changes merged to develop by git flow // ..
    (ve)$ git push


Contributing back
=================

Many of our components in github are open source. In the course of using them, you
might find improvements are necessary or possible. We like having your contributions!

Please  submit a pull request for our review. Although we don't recommend it, if you 
can't wait for our review and merge, you will need to fork that project on github and 
submit your changes to us as soon as the pressure is off. Please do create the pull
request then.

Production Deployments
======================

Our DevOps team are responsible for all production deployments. This enables us
to support the live sites and systems after hours, and ensure that 
infrastructural requirements like backups and monitoring are standardised.

Please note that production deployments need to be booked with the DevOps team
by the appropriate Praekelt project manager, and that we deploy on Mondays
through Thursdays.

.. _BSD 3-Clause Licence: https://raw.github.com/nevir/readable-licenses/master/markdown/BSD3CLAUSE-LICENSE.md
.. _Git Flow: https://github.com/nvie/gitflow
.. _feature branch: http://nvie.com/posts/a-successful-git-branching-model/
.. _pep8: https://pypi.python.org/pypi/pep8
.. _pyflakes: https://pypi.python.org/pypi/pyflakes
.. _What's in a Good Commit?: http://dev.solita.fi/2013/07/04/whats-in-a-good-commit.html
.. _Closing issues via commit messages: https://help.github.com/articles/closing-issues-via-commit-messages
.. _Coverage: https://pypi.python.org/pypi/coverage
