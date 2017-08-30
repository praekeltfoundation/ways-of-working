# HTTPS

[HTTPS](https://en.wikipedia.org/wiki/HTTPS) secures information when it's
being transmitted over the internet. Everybody should use HTTPS, but it is
especially important that we use HTTPS because of the sensitive data we transmit.

## Compatibility

Some of this will be trial and error. Some settings can be tweaked on our side but
some particularly old devices/software will just never work with our system.

It's difficult to anticipate what devices are out there being used in large numbers,
and what browsers are being used on those devices. In a number of cases devices with
old operating systems (like Windows XP, old Android and old BlackBerry OS) will not
be compatible with our HTTPS setup when using the default/built-in browser. If users
have a recent version of a commonly used browser like Google Chrome, Mozilla Firefox,
or Opera Browser installed then that should be compatible.

Users accessing an HTTPS site via a recent version of Opera Mini should not have any
compatibility issues on any platform but the effectiveness of the encrypted connection
is reduced as the connection is decrypted at Opera's servers.

You can use the [SSL Server Test from SSL Labs](https://www.ssllabs.com/ssltest/) with
one of our domains to see the most up-to-date configuration that we support.

### Server Name Indication (SNI) compatibility

The first and most important feature that any device connecting to an HTTPS site on our
cluster will need is Server Name Indication (SNI) support. This, unfortunately, cannot
be worked around and is a strict requirement born out of the fundamental design of the
cluster. Please see [the Wikipedia article](https://en.wikipedia.org/wiki/Server_Name_Indication#Suppor)
for full details.

The native/built-in browsers on the following mobile devices do not support SNI (although
it may be possible for users to install a browser that does support SNI):

- Android 2.3 "Gingerbread" and earlier
- Nokia Symbian OS
- BlackBerry OS 7.1 and earlier

The following browsers on desktop devices do not support SNI:

- Internet Explorer on Windows XP

It's also important to note that the following Python software we use does not support SNI:

- Any Python software running on Python < 2.7.9 (and note that the version of Python 2.7 provided
  with Ubuntu 14.04 is 2.7.6. Also note that our Python Docker containers will always run the
  latest versions of Python)
- Vumi < 0.6.15
- Twisted < 14.0.0

### Transport Layer Security (TLS) compatibility

The load balancer is currently only configured to support some versions of
Transport Layer Security (TLS), namely TLS 1.0, 1.1 and 1.2.

Some older browsers (Internet Explorer 6 or below) do not support our configuration. Once again,
[Wikipedia has a nice table detailing compatibility](https://en.wikipedia.org/wiki/Transport_Layer_Security#Web_browsers).

It's generally a good idea from a security standpoint to only support the latest TLS versions.
We will never support technologies older than TLS 1.0 such as SSL 3.0. We may have to disable
the older versions of TLS that we support as new vulnerabilities are found.

## Enabling HTTPS on Mesos clusters

The SRE team have made it really easy to set up HTTPS with free, automatically renewing
certificates from [Let's Encrypt](https://letsencrypt.org/).

### Rate limits

Let's Encrypt is a free service but ultimately the service has to have some limits.
Please read the [Let's Encrypt documentation](https://letsencrypt.org/docs/rate-limits/) for full details.
The only limit that will be relevant to most people is the "Certificates per Registered Domain" limit.
This limit is set at __20 certificates per week__.

The way this limit works is important to understand: it is applied per registered domain. This means
that it is easy for us to hit the rate limit if we issue certificates for many sites using a wildcard
domain under one of Praekelt's commonly used domain names. For example, a domain like
`seed-message-sender.seed.ng.p16n.org` is actually under the registered domain `p16n.org` - which means
it shares its rate limit with many other Praekelt sites.

tl;dr: If you have a domain that has been bought specifically for your project then you probably
don't need to worry about rate limits. If you are using a domain that ends in `p16n.org` or `unicore.io`
then please speak to SRE before trying to issue a certificate. Certificates are free but not unlimited.

### Setup

Add an application label to the app you want to set up using Mission Control. Right now
only one domain per app is supported.

The label is called `MARATHON_ACME_0_DOMAIN`. Set it to the domain name you want a
certificate for.

A few moments after adding the label the application should be available over HTTPS.

### Redirecting HTTP to HTTPS

Once you've verified that the application works correctly over HTTPS, set the label
`HAPROXY_0_REDIRECT_TO_HTTPS` to `true` to redirect all HTTP traffic to HTTPS.

You must verify that a certificate has been issued and HTTPS is working correctly
before adding the redirect label.

### Using HTTP Strict Transport Security

Another option that you can add for enhanced security is to enable
[HTTP Strict Transport Security](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) (HSTS).
This option improves security when your site is accessed via a modern web browser.
It won't have any effect if your app is an API rather than a website.

You __must__ verify that the certificate and HTTP to HTTPS redirect is working correctly before
enabling HSTS. Once a user's browser "sees" the HSTS header for the first time __it will only connect
to the site via HTTPS for the next 6 months__. This is a thing that is easy to mess up but if your
site has been running with HTTPS and redirects enabled for a while without issues then enabling
HSTS is a good idea.

To enable HSTS, set the application label `HAPROXY_0_USE_HSTS` to a value of `true`.

The HSTS header that is sent does not include the `includeSubDomains` or `preload` directives.
