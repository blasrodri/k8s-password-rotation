# Update your database passwords automatically without downtime

Script to rotate your passwords and k8s secrets automatically.

This is a very simple project. It may - or may not - suit your needs. For a much more
battle tesed, and production grade secret rotation try: [Vault Project](https://www.vaultproject.io/)

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

Since the password of a user will be updated, the script assumes that the client has root
access to the database. By default it will retrieve those credentials through `~/.pgpass` file
(Postgres).

## How to run it

First, modify the `POSTGRES_HOST` environment variable. Eventually we might change this to
be an command line argument directly.

```sh
password_update [options] deployment_name
```
Where `options` can be:
```
-n,--namespace k8s namespace
-nc,--num-chars number of characters that the password will take. Default is 8.
```
