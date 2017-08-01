# Seed stack

The Seed stack is a set of microservices:

- [`seed-control-interface-service`](https://github.com/praekelt/seed-control-interface-service)
- [`seed-message-sender`](https://github.com/praekelt/seed-message-sender)
- [`seed-scheduler`](https://github.com/praekelt/seed-scheduler)
- [`seed-stage-based-messaging`](https://github.com/praekelt/seed-stage-based-messaging)
- [`seed-auth-api`](https://github.com/praekelt/seed-auth-api)
- [`seed-control-interface`](https://github.com/praekelt/seed-control-interface)
- [`seed-identity-store`](https://github.com/praekelt/seed-identity-store)
- [`seed-service-rating`](https://github.com/praekelt/seed-service-rating)

We build [containers for the Seed stack][docker-seed].

Each deployment of the seed stack has a "hub" or "registration" app which contains
logic specific to that country or environment.

[docker-seed]: https://github.com/praekeltfoundation/docker-seed/
