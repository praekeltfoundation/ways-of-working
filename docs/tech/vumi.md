# Vumi

We build on top of our Vumi platform for SMS, USSD and other messaging protocols.

[Vumi][] is a scalable messaging engine which we use for SMS, USSD and other messaging
protocols.

We [build Vumi in a container][docker-vumi] and [push it to Docker Hub][dockerhub].

Nowadays for the most part Vumi is only used via [Junebug][].

## JavaScript sandbox

Apps can be written for Vumi to power messaging campaigns or information systems.
These apps can be written in [JavaScript to run in a sandboxed environment][vumi-jssandbox]
(which is our preferred option) or in Python.

## Vumi Go

[Vumi Go][] is a hosted version of Vumi. Where Vumi gives you the tools to
build large scale messaging applications, Vumi Go provides you with a working
environment that is already integrated into numerous countries.

Vumi Go is deprecated and will not be available after the end of 2017.

[Vumi]: https://github.com/praekelt/vumi
[Junebug]: junebug.html
[docker-vumi]: https://github.com/praekeltfoundation/docker-vumi
[dockerhub]: https://hub.docker.com/r/praekeltfoundation/vumi/
[Vumi Go]: https://vumi-go.readthedocs.org/
[vumi-jssandbox]: https://vumi-jssandbox-toolkit.readthedocs.org/
