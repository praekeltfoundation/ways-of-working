Our project process
===================

The lifecycle of our projects is typically as follows:

1. We produce a Scope of Work for a project, which might not have all the
   technical details, but should be comprehensive enough to list all the
   features so that you can quote on the project's development.
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
5. Your schema changes are expected to be handled by a schema migration script.
6. When work in a feature branch is ready for review then we create a
   pull-request.
7. All collaborators on the GitHub repository are notified of the pull-request
   and will start the process of reviewing the changes.
8. Any issues, concerns or changes raised or recommended are expected to be
   attended to. Once done please notify the reviewers of the changes and
   ask for the changes to be re-reviewed.
9. Once all the changes are approved and one or more of the collaborators
   has left a `:+1:` in the pull-request's comments it can be merged into
   the main branch and is ready for a deploy.

For your code to be ready for review we have the following expectations:

1. It is to be pep8_ compliant and pyflakes_ is not raising any issues.
2. It is to have tests.
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


Production Deployments
======================

Our DevOps team are responsible for all production deployments. This enables us
to support the live sites and systems after hours, and ensure that 
infrastructural requirements like backups and monitoring are standardised.

Please note that production deployments need to be booked with the DevOps team
by the appropriate Praekelt project manager, and that we deploy on Mondays
through Thursdays.

.. _Git Flow: https://github.com/nvie/gitflow
.. _feature branch: http://nvie.com/posts/a-successful-git-branching-model/
.. _pep8: https://pypi.python.org/pypi/pep8
.. _pyflakes: https://pypi.python.org/pypi/pyflakes
