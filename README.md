pgb
===

Simple utility to manipulate docker container and serve postgres on localhost
for test or development.

setup
=====

With docker installed and running on localhost use following commands to setup
postgres `9.5.4`:

```bash
git clone git@github.com:dleemoo/pgb.git SOMEDIR &&
cd SOMEDIR &&
rake setup VERSION=9.5.4
```

The `postgres:9.5.4` image will be pulled from docker hub and a
`docker-copose.yml` is generated.

usage
=====

To start the previous container setup, run:

```bash
cd SOMEDIR
rake start
```

Install `psql` in the host machine or connect your app with right postgres
image credentials (defauts to `postgres` user with empty `password`).

If you prefer, setup `~/.pgpass` to login with a simple `psql`:

```
localhost:5432:*:postgres:
```
