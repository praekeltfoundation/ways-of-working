# RapidPro

[CasePro](https://github.com/rapidpro/rapidpro) is an open-source
Django application for messaging.

## Tips

### Adding credits

We don't normally use credits because we host our own RapidPro instances and are
billed by our SMS providers.

The permissions for adding credits are a bit strange. Administrators can't add
credits, you need to be a Django superuser. You can do this in a Python shell
or in the database.

Once you're a superuser, it's _really_ hard to find the interface for adding
an arbitrary Top Up.

You can go to `/org/update/1/` and get a button to go to the Top Ups interface
where you can add a new Top Up.

The maximum number of credits in a Top Up is the size of an `IntegerField` in
Django, which is 2147483647.
