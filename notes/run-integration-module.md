# How to start Integrations module locally

## Run `flatfile` functionality

- Able to download the user/aplicants information as `csv` file

```bash
# Run the following services:

# Please ask team members to copy and paste the credentials and past into a `.env` (please create it if not yet) file under cmd/svc-integrations folder
# svc-integrations
TARGET=svc-integrations mk aws.migrate.down && TARGET=svc-integrations mk aws.migrate.up && TARGET=svc-integrations AUTH_ENABLED=true mk compose.up.build APP_BACKGROUND_WORKER_ENABLED=1
# svc-hr
mk vendor && TARGET=svc-hr mk aws.migrate.down && TARGET=svc-hr mk aws.migrate.up && TARGET=svc-hr mk aws.seed && TARGET=svc-hr mk data
TARGET=svc-hr mk compose.up.build
# svc-dir
TARGET=svc-dir mk aws.migrate.down && TARGET=svc-dir mk aws.migrate.up && TARGET=svc-dir mk compose.up.build
# svc-query
TARGET=svc-query mk compose.up.build
# svc-url
TARGET=svc-url mk mysql.migrate
TARGET=svc-url AUTH_ENABLED=1 mk compose.up.build
# svc-award
TARGET=svc-award mk aws.migrate.down && TARGET=svc-award mk aws.migrate.up && TARGET=svc-award mk compose.up.build
# svc-payrate
TARGET=svc-payrate mk aws.migrate.down && TARGET=svc-payrate mk aws.migrate.up && TARGET=svc-payrate mk compose.up.build
go run cmd/svc-payrate/dev/seed/main.go all
# svc-backstage -> For this service, no need to run since devbox already run it

# Then, please ensure the deputy-webapp is up and running
# For HR team, please run `make upbdi` for deputy-webapp
make upbdi
make fe.dev
# And then, please ensure the devbox is up and running
make upd
```

Please follow the  original setup [documentat](https://deputy.atlassian.net/wiki/spaces/COMPLIANCE/pages/3626730237/FlatFile+Local+setup) for the local testings
