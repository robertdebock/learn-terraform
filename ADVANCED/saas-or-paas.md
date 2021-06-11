# SaaS or PaaS

|expected time|requirements|
|-------------|------------|
|30 minutes   |none.       |

Goal: Make a conscious, balanced decision when using Saas services

## Explanation

Most cloud providers offer lots of services that can be used to compose your infrastructure. Think of these services:

- Database as a service.
- Kubernetes cluster as a service.
- DNS as a service.

It's typically easy to use these service, sometimes it's even cheaper, although mostly it's more expensive.

You can also build these services yourself.

|Advantage of PAAS  |Disadvantage of PAAS              |
|-------------------|----------------------------------|
|Works on any cloud.|Requires more technical expertise.|
|Can be cheaper.    |You're responsible yourself.      |

If you build services yourself, think about these potential issues:

- Needs to be coded and maintained yourself.
- Because there is no clear provider-consumer model, the interface can be unclear.
- Tests need to be created, and run frequently.
- Compliance is you yourself to fix. (Can be an advantage.)

## Questions

1. What's your preference?
2. Can you prevent cloud-lock-in?
3. Would a hybrid model work?
