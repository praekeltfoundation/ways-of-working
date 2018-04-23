# CasePro

[CasePro](https://github.com/rapidpro/casepro) is an open-source
Django application for helpdesk and case management.

It's made by the same organisation that builds RapidPro.

## Pods

CasePro pods allow you to display custom data in the CasePro
interface without merging it into the CasePro codebase.

Currently you can only add information to the case detail view.

Pods can be installed in the project as Python packages and added to
the `PODS` array in settings.

### Registration pod

Our [registration pod][] retrieves user data from our seed microservices and
displays it next to the open case.

### Subscription pod

Our [subscription pod][] displays information about the user's subscriptions
from our stage-based-messaging service.

[registration pod]: https://github.com/praekelt/casepropods.family_connect_registration/
[subscription pod]: https://github.com/praekelt/casepropods.family_connect_subscription/
