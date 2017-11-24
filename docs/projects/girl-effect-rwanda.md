# Girl Effect Rwanda

Girl Effect Rwanda is a project to improve the lives of women and girls in Rwanda.

## Publishing

The mobile site runs at <http://www.ninyampinga.com/> and is hosted in South Africa.

## Messaging

We use Vumi Go to interact with users.

### SMS

The shortcode 1019 is used to send and receive SMS messages.

We [connect Vumi Go to Mtech using SMPP][sms_mtech] and they provide aggregation for Tigo and Airtel users. For MTN users, we establish an IPsec connection to MTN on `vumi-gateway` and [then connect Vumi Go using SMPP][sms_mtn].

### USSD

The USSD code is `*900#`.

[sms_mtech]: https://github.com/praekelt/puppet/blob/develop/modules/vumigo_prod/files/mtech_rw_smpp_transport.yaml
[sms_mtn]: https://github.com/praekelt/puppet/blob/develop/modules/vumigo_prod/files/mtn_rw_sms_transport.yaml
