# PhEMA Workbench Deployment Config

Docker resources to set up a PhEMA Workbench instance.

## Prerequisites

You'll need [Docker](https://www.docker.com/) and [Docker
Compose](https://docs.docker.com/compose/) installed.

## Local Deploy

To run the workbench locally, first clone this repo:

```
git clone https://github.com/PheMA/phema-workbench-deploy.git && cd phema-workbench-deploy
```

Then spin up the containers with Compose:

```
PHEMA_WORKBENCH_CERTS_PATH=./certs PHEMA_WORKBENCH_HTPASSWD_PATH=./htpasswd docker compose up
```

The environment variables provided point to local, testing versions of the `.htpasswd` file and SSL certificates.  None of these should be used in a publicly-facing environment.

:bulb: You may have to run this a few times until it works, since container
dependencies are not currently set up properly. Once Postgres is initialized it
should start up first time every time.

### Access

Once the containers are all running, the following URLs should be accessible:

* https://workbench.local.phema.science:4321/ - The PhEMA Workbench app
* https://workbench.local.phema.science:4321/fhir - The FHIR server base URL
* https://workbench.local.phema.science:4321/hapi - The HAPI FHIR web overlay

:bulb: When running CQL, use the **PhEMA Workbench CQL Executor** server.

#### Workbench Credentials

For the local instance, the default credentials are:

* **Login:** test
* **Password:** test

## Production Deploy

We have the ability to perform a production deploy protected by basic auth (for
now). To do this, you need to set the following environment variables before
running Compose:

1. `PHEMA_WORKBENCH_HTPASSWD_PATH`: The path to the [`htpasswd`](https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/) file to use.
2. `PHEMA_WORKBENCH_ENV`: Set this to `prod` to use the `nginx-prod.conf` file,
   or create a new Nginx config file called `nginx-whatever.conf` and set the
   variable to `whatever`.

For example:

```
PHEMA_WORKBENCH_HTPASSWD_PATH=/opt/phema/workbench/.htpasswd PHEMA_WORKBENCH_ENV=prod docker-compose up
```