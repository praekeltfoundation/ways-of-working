Our Platforms
=============

Praekelt uses two main platforms for the bulk of engineering work:

1. Django

   We use Django for websites, mobi sites, responsive sites, mobi HTML5 apps.

2. Vumi

   We use our Vumi platform for SMS, USSD and other messaging protocols.

Use of any other platform must be approved by our engineering management, and may
need to be hosted separately from our usual environments, so please get this
sorted out prior to commencing development on a project.

Django
------

You should use the latest stable release of Django *as of the start of the project* 
unless otherwise specified. Pin that version in your requirements so that the
project won't break by accidently being deployed on a newer version without
testing.

We deploy Django in the following stack:

- Ubuntu Server (current LTS release)
- haproxy_ for load balancing where appropriate
- nginx_
- gunicorn_
- supervisord_
- postgresql_

For development, you can simplify this, and for QA we won't bother about haproxy
but the rest of the stack will be required for QA so we recommend you keep your
dev environment as close to this as you can.

Notes:

- We manage hostnames in nginx, because there may be multiple QA and live hostnames
  so don't use Django's ALLOWED_HOSTS.
- Make use of pip and virtualenv
- Avoid using CachedStaticFilesStorage, or generating CSS/JS automatically as this
  breaks load balanced environments.
- There are specific requirements for logging. Please see the Logging_ section
  for more information.

.. _haproxy: http://haproxy.1wt.eu/
.. _nginx: http://nginx.org/
.. _gunicorn: http://gunicorn.org/
.. _supervisord: http://supervisord.org/
.. _postgresql: http://www.postgresql.org/

Vumi
----

Vumi_ is a scalable messaging engine which we use for SMS, USSD and other messaging
protocols.

Vumi Go is a hosted version of Vumi. Where Vumi gives you the tools to 
build large scale messaging applications, Vumi Go provides you with a working 
environment that is already integrated into numerous countries.

Apps can be written for Vumi Go, to power messaging campaigns or information systems.
These apps can be written in Javascript to run in a sandboxed environment (which is
our preferred option) or in Python.

See the `Vumi Go`_ documentation as well as the `JS Sandbox toolkit`_ documentation for
writing apps.

.. _Vumi: http://vumi.org/
.. _Vumi Go: http://vumi-go.readthedocs.org/
.. _JS Sandbox toolkit: http://vumi-jssandbox-toolkit.readthedocs.org/

Logging
-------

All logging must happen to a standardized path, under */var/praekelt/logs*. If your app
has a large amount of files (celery, worker, and app, for instance), write each of
these to a named path under */var/praekelt/logs/appname/foo.log*, otherwise just 
*/var/praekelt/logs/foo.log* is sufficient.

Logs always end with the extension *.log*. *.err* is not valid. If you need to write out
error logs, either use the name *foo-error.log*, or write your supervisodrd_ configuration
with the *redirect_stderr* option.

The basis for this requirement is to ease debugging (hunting logs in 7 different
directories is never fun, and causes issues when under time pressure), simplifies log
rotation, and allows them to easily fit within our automatic log collection and 
indexing system.
