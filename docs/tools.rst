Tools we use
============

The following are tools we use on a regular basis and which we expect
you to either use or at least be very familiar with.


Git
---

We use Git, if you work with us, you will use Git and GitHub.
There is no exception.

Provide us with your GitHub username and we will provide you with a
repository to work on. All repositories are to be hosted under the
`Praekelt Organization`_ on GitHub.

Issues & Tickets
----------------

For projects that are not open-source we use Jira_. You will be given an
account to use which will have access to the relevant projects.

For all our open-source projects we use GitHub_ issues on the repository
that the work is going on in.

For development, if there is no ticket it does not exist.
Make sure the work you are doing has a ticket and is being tracked.
Stop working and protest immediately if people are treating your mailbox
as their ticketing system. We're tried that, it does not work.

A ticket should represent a solid piece of work you intend to do.
Make an effort to keep the work you are trying to do to 16 hours.

Any estimate you make for actual work done beyond 16 hours is assumed to be

a) largely thumb-suck.
b) going to be very hard to review.

Make an effort to keep it to 16 hours.

Git Flow
--------

We use the `Git Flow`_ branching model as part of our development.
It's a convenient way to manage your branches.

Have a read through the `blog <http://nvie.com/posts/a-successful-git-branching-model/>`_
post describing the general idea and follow the installation instructions
in the repository to install it for your development platform of choice.

Hub
---

We use Hub_ to interface with GitHub_'s API. Use it allows one to turn issues
on GitHub into pull-requests. If that is done then once the pull-request is
merged into the main branch the issue is automatically closed.

Sentry
------

We have a dedicated Sentry_ instance for our projects. You are expected to
configure your application to make use of this for error reporting.

You will be given access to your Sentry project and access tokens to will be
made available for you to configure your application's client with.

Puppet
------

We try an automate as much as possible, this includes our hosting environment.
You will need to give us your SSH key so we can provision a machine for your
project. Generally you will be given access to a machine that is to be
used for QA_ and one that is to be used for the production environment.

These machines are provisioned using Puppet_. You will not get access to our
puppet repository. If you need specific software installed on your machine
that it was not provisioned with then please ask for it to be added.
Do not install it yourself without notifying us. This would break our
assumption that every machine can be provisioned from scratch with puppet.

If the machine you've been working on needs to be rebuilt and you've made
changes that are not in puppet then it'll be provisioned without those changes.

Databases / data stores
-----------------------

We use the following services to store our data. Not all projects will use
all of them but generally a number of these will be involved.

1. PostgreSQL_
2. Riak_
3. Memcached_
4. Redis_
5. Neo4J_

These will be made available to you on a per project basis. Puppet ensures
that each of these are backed up.

South
-----

For Django applications, some applications are mandatory:

1. Sentry_ for application reporting.
2. South_ for managing database schema changes.
3. Nose_ for running tests.
4. Haystack_ for search.
5. Memcached_ for caching.

Graphite
--------

We use Graphite_ for the majority of our metrics. You will be given details
for the Graphite_ server and how metrics are to be published to it.

IRC
---

IRC is our team's communication tool of choice. Join us in ``#vumi`` or
``#jmbo`` on irc://irc.freenode.net/.

Various tools report into these channels and provide insight into what is
going on.


.. _Praekelt Organization: https://github.com/praekelt/
.. _Git Flow: https://github.com/nvie/gitflow
.. _GitHub: https://github.com/
.. _Jira: https://praekelt.atlassian.net/
.. _Sentry: https://github.com/getsentry/sentry/
.. _PostgreSQL: http://postgresql.org/
.. _Riak: http://basho.com/riak/
.. _Memcached: http://memcached.org/
.. _Redis: http://redis.io
.. _Neo4J: http://neo4j.org
.. _QA: http://en.wikipedia.org/wiki/Quality_assurance
.. _Hub: http://defunkt.io/hub/
.. _Nose: https://nose.readthedocs.org/
.. _South: http://south.aeracode.org/
.. _Haystack: http://haystacksearch.org/
.. _Graphite: http://graphite.wikidot.com/
