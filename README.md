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
docker-compose up
```

:bulb: You may have to run this a few times until it works, since container
dependencies are not currently set up properly. Once Postgres is initialized it
should start up first time every time.

### Access

Once the containers are all running, the following URLs should be accessible:

* http://workbench.local.phema.science/ - The PhEMA Workbench app
* http://workbench.local.phema.science/fhir - The FHIR server base URL
* http://workbench.local.phema.science/hapi - The HAPI FHIR web overlay

:bulb: When running CQL, use the **PhEMA Workbench CQL Executor** server.