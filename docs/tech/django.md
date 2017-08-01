# Django

We use the [Django][] Python framework heavily.

You should use the latest stable release of Django *as of the start of the project*
unless otherwise specified. Pin that version in your requirements so that the
project won't break by accidentally being deployed on a newer version without
testing.

You should build Docker containers for your Django app using [django-bootstrap][]
as a base:

```
FROM praekeltfoundation/django-bootstrap:py3
```

[Django]: https://www.djangoproject.com/
[django-bootstrap]: https://hub.docker.com/r/praekeltfoundation/django-bootstrap/
