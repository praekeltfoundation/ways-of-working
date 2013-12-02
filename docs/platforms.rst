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

You should use the latest stable release of Django unless otherwise specified.

We deploy Django in the following stack:

- Ubuntu Server (current LTS release)
- haproxy for load balancing where appropriate
- nginx
- gunicorn
- supervisord
- postgresql

For development, you can simplify this, and for QA we won't bother about haproxy
but the rest of the stack will be required for QA so we recommend you keep your
dev environment as close to this as you can.

Notes:

- We manage hostnames in nginx, because there may be multiple QA and live hostnames
  so don't use Django's ALLOWED_HOSTS.


Vumi
----

Vumi_ is a scalable messaging engine which we use for SMS, USSD and other messaging
protocols. Vumi Go is a hosted version of Vumi. Where Vumi gives you the tools to 
build large scale messaging applications, Vumi Go provides you with a working 
environment that is already integrated into numerous countries.

Apps can be written for Vumi Go, to power messaging campaigns or information systems.
These apps can be written in Javascript to run in a sandboxed environment (which is
our preferred option) or in Python.

See the `Vumi Go`_ documentation regarding writing apps, and there is documentation
for a `state machine`_ for USSD as well.

.. _Vumi: http://vumi.org/
.. _Vumi Go: http://vumi-go.readthedocs.org/
.. _state machine: http://vumi-jssandbox-toolkit.readthedocs.org/
