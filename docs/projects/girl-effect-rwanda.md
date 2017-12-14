# Girl Effect Rwanda

Girl Effect Rwanda is a project to improve the lives of women and girls in Rwanda.

## Publishing

The mobile site runs at <http://www.ninyampinga.com/> and is hosted in South Africa.

## Messaging

We use RapidPro and Junebug to interact with users.

RapidPro and Junebug run in 3 containers in South Africa:

- RapidPro web
- RapidPro celery
- Junebug

### SMS

We use the shortcode 1019 to send and receive SMS messages.

We have [Junebug config][junebug_config] for both Mtech and MTN.

- Mtech is an aggregator for Tigo and Airtel users and we connect directly to them over SMPP
- MTN require that we establish an IPsec connection from `vumi-gateway` and then connect over SMPP

### USSD

The USSD code is `*900#`.

[junebug_config]: https://github.com/praekeltfoundation/girleffect-rwanda-config
