Tools we use
============

The following are tools we use on a regular basis and which we expect
you to either use or at least be very familiar with.

IRC
---

IRC is our team's communication tool of choice. Join us in ``#prk-dev`` for general
developer support, or ``#vumi`` or ``#jmbo`` for development of those platforms,
on irc://irc.freenode.net/.

Various tools report into these channels and provide insight into what is
going on.

Git
---

We use Git. If you work with us, you will use Git for revision control,
and GitHub. There is no exception.

Provide us with your GitHub username and we will provide you with a
repository to work on. All repositories are to be hosted under the
`Praekelt Organization`_ on GitHub.

**Please** read `What's in a Good Commit? <http://dev.solita.fi/2013/07/04/whats-in-a-good-commit.html>`_
for a good introduction to effective use of version control commits.

**Avoid these:**

- Don't commit merge conflicts. See `the Pro Git book on merge conflicts <http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging#Basic-Merge-Conflicts>`_
- Don't commit snapshots. Only make one change per commit. **Read What's in a Good Commit above.**
- Don't commit large content files. Manage them in the CMS.

git-flow
--------

We use the `git-flow`_ branching model as part of our development.
It's a convenient way to manage your branches. You are not required to use
Git Flow but you are required to follow naming conventions it sets
with regard to branch names and prefixes.

Have a read through the `blog <http://nvie.com/posts/a-successful-git-branching-model/>`_
post describing the general idea and follow the installation instructions
in the repository to install it for your development platform of choice.

Unless you've explicitly been told otherwise, we require our team to review
your code before landing it in the develop branch.
Please provide pull requests for our review, the command line tool Hub_ (see below) is
a convenient way of turning GitHub issues into pull-requests.

The pull-request requirement still remains when using Jira_. You can still
use Hub_ - however your Jira_ ticket's status will not automatically change
when the feature branch lands, so you will need to update this yourself.

Please read `Useful Github Patterns <http://blog.quickpeople.co.uk/2013/07/10/useful-github-patterns/>`_
to see ways of working with branches and pull requests that we like.

HubFlow
-------

Hubflow is an adapted version of Gitflow, specifically tailored for use with Github.

It provides the usefulness of `git-flow`_ with Github goodness embedded.

For more information on that, see this link: `Hubflow <https://datasift.github.io/gitflow/>`_

Hub
---

For projects with issues tracked in Github issues, We use Hub_ to interface
with GitHub_'s API. It allows one to turn issues on GitHub into
pull-requests. If that is done then once the pull-request is merged into
the main branch the issue is automatically closed.

We use the `git_flow`_ branching model as part of our development.
It's a convenient way to manage your branches. You are not required to use
Git Flow but you are required to follow naming conventions it sets
with regard to branch names and prefixes.

Issues & Tickets
----------------

For project work we use Jira_. Only our core open-source platforms maintain
their issues in the GitHub repository.

You will be given an account to use which will have access to the relevant
projects.

For development, if there is no ticket it does not exist.
Make sure the work you are doing has a ticket and is being tracked.
Stop working and protest immediately if people are treating your mailbox
as their ticketing system. We've tried that, it does not work.

If a Jira project has a workflow, you need to update your tickets
appropriately:
New -> Open -> Fixed in dev (when pushed to github) -> Deployed to QA

Our QA team will move the ticket to QA Passed, and our DevOps team will be
responsible for the production deployment before the ticket is resolved.

If a ticket is QA Failed then it's back into your section of the workflow.

A ticket should represent a solid piece of work you intend to do.
Make an effort to keep the work you are trying to do in one ticket to no more
than 16 hours.

Any estimate you make for actual work done beyond 16 hours is assumed to be

a) largely thumb-suck.
b) going to be very hard to review.

Make an effort to keep it to 16 hours or break it up unto multiple tickets
each representing 16 hours of work.

Sentry
------

We have a dedicated Sentry_ instance for our projects. You are expected to
configure your application to make use of this for error reporting.

You will be given access to your Sentry project and access tokens to will be
made available for you to configure your application's client with.

Puppet
------

We try and automate as much as possible, this includes our hosting environment.
You will need to give us your SSH key so we can provision a machine for your
project. Generally you will be given access to a machine that is to be
used for QA_. Since our DevOps team do the production deployments, and you will
get access to production error reports via Sentry_, you won't get access to
production without a valid need for troubleshooting, and then it will be without
sudo access.

These machines are provisioned using Puppet_. You will not get access to our
puppet repository. If you need specific software installed on your machine
that it was not provisioned with then please ask for it to be added.
Do not install it yourself without notifying us. This would break our
assumption that every machine can be provisioned from scratch with puppet.

If the machine you've been working on needs to be rebuilt and you've made
changes that are not in puppet then it'll be provisioned without those changes.

Sideloader
----------

Our DevOps team automate deploys using Sideloader, our tool that creates
deb packages from github repos. To enable a repo for this deploy
automation, create a .deploy.yaml file in your repository, listing
dependencies and scripts.

We then use puppet to install the debs whenever a new one is published.
Ask our DevOps team for help with Sideloader, and to set up the puppet
automation to install the debs.

We can optionally set up a post commit hook to deploy any changes that are
pushed to the develop branch, to QA - if you're feeling lucky...

See `Sideloader help`_ for more info (requires login via github).


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

Django Applications
-------------------

For Django applications, some applications are mandatory:

1. Sentry_ for application reporting.
2. 
3. Nose_ for running tests.
4. Haystack_ for search.
5. Memcached_ for caching.

We strongly recommend you use our sample django-skeleton_ as a starting point for
Django projects, as it has some of these already included.

Translations
------------

We use Gettext or translations in shell scripts, applications and web pages.
Read more about Gettext along with some examples on Wikipedia:
http://en.wikipedia.org/wiki/Gettext

In Django, Gettext is used by default for translations, utilizing
ugettext_lazy for models.py and ugettext in other places. We like
{% trans %} and {% blocktrans %} tags and enforce these for our
open source products.

Graphite
--------

We use Graphite_ for the majority of our metric publishing for dashboards.
If appropriate, you will be given details for the Graphite_ server and how
metrics are to be published to it.


Front-end
---------

Sass_ CSS pre-processor so that we can take advantage of things that CSS doesn't have yet, or doesn't do properly: variables; nesting (used sparingly); CSS partials / includes; media queries used more like element queries; mixins.

JavaScript task runners like Grunt_ and Gulp_, with lots of plugins. These handle code linting, image minification, processing Sass into CSS, concatenation and minification of CSS and JS, and running tests.

.. _Praekelt Organization: https://github.com/praekelt/
.. _git-flow: https://github.com/nvie/gitflow
.. _hubflow: https://datasift.github.io/gitflow/
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
.. _Sideloader help: http://sideloader.praekelt.com/help/
.. _django-skeleton: https://github.com/praekelt/django-skeleton/#django-skeleton
.. _Sass: http://sass-lang.com/
.. _Grunt: http://gruntjs.com/
.. _Gulp: http://gulpjs.com/
