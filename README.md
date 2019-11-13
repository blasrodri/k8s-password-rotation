# Update your database passwords automatically without downtime

Script to rotate your passwords and k8s secrets automatically.

At the moment, it only supports:
+ Kubernetes
+ Postgres
+ pwgen

## Assumptions

Each application loads all the necessary database credentials from kubernetes secrets.
So, in order to avoid donwtime, there are two secrets per application. Thus, every time
we want to update the password, only the credentials that are not currently being used
are the ones rotated. This ensures that the application never ends up in a state where
tries to use old credentials.

