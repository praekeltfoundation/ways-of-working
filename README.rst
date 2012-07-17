Praekelt Foundation Dev Ways of Working
=======================================


Core tools
----------

* JIRA - issue tracker
* Virtualenv - sandboxed Python modules, great for project specific development environments
* Puppet & Fabric - system automation recipes
* Git, Git Flow & Github - version control
* Munin - keep tabs on your services
* Sentry - Python logging
* Supervisord - keep services running

Sprints
-------

A lot of our projects as a Foundation are long-running. Vumi as a hosted platform, TxtAlert and the Gates Foundation projects as services built on top of it and Young Africa Live are very much projects with long-running goals.

In order to reach our long running goals we strive to work with two week sprints. At the start of a sprint we will determine the various project priorities, assign tickets along with hour estimates that describe the work involved. The aim is to release stable new features at the end of every two week sprint, regardless of the size of the features introduced.

Sprints result in one or more deploys. We should be comfortable with deploying, deploys should happen on a regular basis to prevent them becoming scary events. Delays in deploys have the tendency to result in small changes piling up and becoming big changes of which the side-effects are difficult to assess.

Jira
----

For every significant bit of work make sure there’s a ticket in Jira (bug, feature, improvement, task etc...).

Tickets should never amount more than 16 hours of work, anything larger is unpredictable and should be split into smaller sub-tasks, each of max 16 hours.

Git
---

We use the `Git Flow`_ branching model as part of our development. Large undertakings (with or without subtasks) should:

* Have a dedicated feature branch in Git. 
* Have the branch name reflect the ticket number in Jira, for example “feature/VUMI-13-smpp-failure-handling”. Where “VUMI-13” is the Jira ticket and “smpp-failure-handling” is the short description of what the ticket is about.

Git Flow provides a few helper scripts for creating an managing development going on in feature branches.

Here’s a sample transcript of starting a feature branch for new development and closing it again and merging all the work done back into the main development branch::

    $  git flow feature start VUMI-13-transport-failure-handling
    Switched to a new branch 'feature/VUMI-13-transport-failure-handling'

    Summary of actions:
    - A new branch 'feature/VUMI-13-transport-failure-handling' was created, based on 'develop'
    - You are now on branch 'feature/VUMI-13-transport-failure-handling'

    Now, start committing on your feature. When done, use:

         git flow feature finish VUMI-13-transport-failure-handling

At this point you start writing all your code and associated tests and commit your changes to your feature branch. While you’ve been working on your feature branch some of your colleagues will have introduce new changes to the develop branch since you started your feature branch. Before you merge your work back into the main develop branch you’ll need to pull in those changes to make sure none of your new contributions will break with the changes made.
Git allows you to do with easily with ‘rebase’::

    $  git rebase develop

This could introduce some file conflicts which you can resolve with ‘git mergetool’. Fix any conflicts that might be introduced and run all your tests again. When your tests pass then run the following command to close your feature branch and merge all your work into the main develop branch::

    $  git flow feature finish VUMI-13-transport-failure-handling
    Switched to branch 'develop'
    Deleted branch feature/VUMI-13-transport-failure-handling (was 0bd082a).

    Summary of actions:
    - The feature branch 'feature/VUMI-13-transport-failure-handling' was merged into 'develop'
    - Feature branch 'feature/VUMI-13-transport-failure-handling' has been removed
    - You are now on branch 'develop'

At this point do a ‘git push’ and your changes will be pushed to the repository and are then available to the whole team.

If you find that you need to share work you’re currently doing in a feature branch you can use ‘git flow feature publish <name of branch>’ to publish your feature branch in the repository without merging it into develop. 

Sentry
------

Python logging should be handled by `Praekelt's Sentry instance <http://sentry.praekelt.com>`_ for easy/central web access.  

Sentry supports the ability to directly tie into Python's logging module. To use it simply add the `Raven <http://raven.readthedocs.org/en/latest/index.html>`_ Python client's ``SentryHandler`` to your logger::

    from raven.conf import setup_logging
    from raven.handlers.logging import SentryHandler

    setup_logging(SentryHandler('http://public:secret@example.com/1'))

A recommended pattern in logging is to simply reference the modules name for each logger. So for example, you might at the top of your module define the following::

    import logging
    logger = logging.getLogger(__name__)

See Raven's `configuring logging docs <https://raven.readthedocs.org/en/latest/config/logging.html>`_ for more info.

For web applications you can hook up Django specifically as described in Sentry's `configuring Django docs <https://raven.readthedocs.org/en/latest/config/django.html>`_.

To log Django management command errors to Sentry alter your ``manage.py`` to read as follows::

    #!/usr/bin/env python
    import logging
    import traceback
    import os
    import sys

    if __name__ == "__main__":
        os.environ.setdefault("DJANGO_SETTINGS_MODULE", "project.settings")

        from django.core.management import execute_from_command_line

        try:
            execute_from_command_line(sys.argv)
        except Exception, e:
            exc_info = sys.exc_info()
            logging.error(e, exc_info=exc_info)
            traceback.print_exc()


Test Coverage
-------------

100% test coverage is a pipe dream, don’t waste your time pursuing it. That said, we should have enough test coverage and we should monitor our test coverage statistics.

Rule of thumb: all important moving parts of our applications should be tested. You, from your point of view, define what is important.

We do:
~~~~~~

* We test APIs
* We test magic features which could have side-effects (Django’s signals!)
* We test core operations of our applications 
* Do we send an SMS when asked to?
* Do we throttle as expected?
* Do we prevent duplicate SMS sending when asked to?
* We go to lengths in mocking our service oriented architecture’s actors to enable our tests.

We don’t
~~~~~~~~

* We don’t test trivial things that aren’t mission critical to our application.
* We don’t retest what our programming languages to for us anyway, int(“1”) == 1 for example.
* We don’t test for tests’ sake.

We are all responsible for maintaining our tests. As a rule of thumb, if your code breaks in QA because of someone else’s change then your test coverage was inadequate. Your test coverage should help your colleagues from making sure their changes don’t break stuff. Please write your tests with this in mind. Tests will save you time and headaches. Insufficient test coverage means you’ll be delaying your colleagues’ changes while you’re chasing bugs in your code base. It is your responsibility.

Deploying
---------

We’ve used fabric to automate our deployments but we need to rethink how we do that. It was a home grown solution and it was never loved. We’ll be using git flow’s versioned releases as a starting point for our deployments. This will prevent some of the problems we’ve been having where teams (other than ourselves) are running our Vumi code base off of the develop branch and who are then very susceptible to code breaking because of the frequency of changes being introduced.

Our starting point for that switch is 1st of August.

We use Puppet to provision our machines. We maintain a VirtualBox Ubuntu 10.04 / Lucid image in the repository, using Vagrant we can easily provision this VM with the latest code and use it for testing and development. It is also a quick an easy way for someone who’s completely new to Vumi to get introduced to a working system.

.. _Git flow: https://github.com/nvie/gitflow

Jmbo
----

Stack::

* Python 2.6 or 2.7 , Django 1.3.1, PostgreSQL >= 8.4, memcached, supervisor, nginx, gunicorn, buildout.
* Code lives in /var/praekelt owned by the www-data user.

The script located at 
https://github.com/praekelt/jmbo-skeleton/blob/master/scripts/create-jmbo-project.sh 
creates a new Jmbo Go project from templates. It is a friendlier replacement for 
jmbo-paste.

The script located at 
https://github.com/praekelt/jmbo-skeleton/blob/master/scripts/setup-server.sh 
prepares a clean Ubuntu 12.04 server to host Jmbo. 

The script located at 
https://github.com/praekelt/jmbo-skeleton/blob/master/scripts/deploy-project.sh 
deploys Jmbo instances to the /var/praekelt directory. It takes a number of 
command-line arguments to control the deployment.

The ideas contained in the last two scripts will be translated to puppet in the near
future; however, these scripts will always be maintained as a reference for
third-party developers.

