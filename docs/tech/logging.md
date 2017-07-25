# Logging

All logging must happen to a standardized path, under `/var/praekelt/logs`. If your app
has a large amount of files (celery, worker, and app, for instance), write each of
these to a named path under `/var/praekelt/logs/appname/foo.log`, otherwise just
`/var/praekelt/logs/foo.log` is sufficient.

Logs always end with the extension `.log`. `.err` is not valid. If you need to write out
error logs, either use the name `foo-error.log`, or write your supervisord configuration
with the `redirect_stderr` option.

The basis for this requirement is to ease debugging (hunting logs in 7 different
directories is never fun, and causes issues when under time pressure), simplifies log
rotation, and allows them to easily fit within our automatic log collection and
indexing system.
