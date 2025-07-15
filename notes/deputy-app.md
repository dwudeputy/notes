# Onboarding Note

## 1. Setup `deputy-webapp` codebase for local development environment

<!-- Using shift + cmd + v to preview the README file contents -->
There are few steps which require for setting up [deputy-webapp](https://github.com/DeputyApp/deputy-webapp) codebase

(1). Please ensure you have installed exact node & docker veriosn,

- Node version: `v18.16.0` by running this command:

```bash
brew install nvm
nvm install v18.16.0
nvm use v18.16.0
nvm alias default v18.16.0
```

- Docker version: `27.5.1` for now (Let's use current version for now, which can be explored by using new docker version 📋)

```bash
# Go to https://docs.docker.com/desktop/release-notes/#4380
# Find the versuib 4.38.0 and download it for your Mac/Windows version
# After installed the docker version and should look like this:
Server: Docker Desktop 4.38.0 (181591)
 Engine:
  Version:          27.5.1
```

(2). After cloned the codebase from deputy originzation github, there are few steps for starting up the deputy-webapp app locally,

- Install all dependencies, here are the commands:

```bash
make fe.install # install the npm packages for the deputy-webapp codebase
make fe.build # need to build the 
make upd # to start with docker containers for deputy-webapp to start to run
make seed # to seed some mock data for the deputy-webapp to display
make fe.dev # start to
# Sometimes, we might need to consider to debug for local codebase, there are few commands we could also run:
# under the deputy-webapp root level of project folder
npm run vue:static # for build the vnext (Vue 3) project
```


## 2. `devbox` codebase setup

- `devbox` is used for enabling software engineers to run the `deputy-webapp` and other parts of the Deputy ecosystem on their local machines.

About the [devbox github instruction](https://github.com/DeputyApp/devbox?tab=readme-ov-file#devbox)

```bash
# setup commands
git clone git@github.com:DeputyApp/devbox.git $HOME/dev/src/github.com/deputyapp/devbox # clone teh repo
brew install mysql mkcert nss # reuqired libs
mkcert --install # create a local certificate authority
make certs.create # issue a certificate
# run commands
make dns # try to make local site domain url: (https://business.dev.local.dpty.io) load a bit more faster
make upd # start with devbox related docker containers
# make upbd # for rebuild only - update docker containers
# TO BE CONTINUED
```

## 3. `go-svc` & sub-services setup

- `go-svc`: is the codebase which run bunch of services ~

About the [go-sv github instruction](https://github.com/DeputyApp/go-svc?tab=readme-ov-file#1-clone-the-repo)


### Sub module `svc-hr` setup

- `svc-hr`: is the modules for deuty-webapp `people` tab related functionality

```bash
# Apply for a ngrok url from https://dashboard.ngrok.com/domains
# CLick `+ New Domain` to apply for a new ngrok domain
# Once applied ngrok domain successfully, The URL should be looking like this:
# eg: xxx-xxx.ngrok-free.app
# Run the below command to start ngrok:
ngrok http --url=internally-quick-boxer.ngrok-free.app 8888 # port 8888 refers to graphql access
# Next step: Go to svc-hire/.env file and paste the secrets for the local
cd go-svc
cd nano ./cmd/svc-hr/.env
# Then, paste these credentials into the file: svc-hr/.env
APP_DEPUTY_GRAPHQL_PROXY_JWT_KEY=ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
APP_DEPUTY_GRAPHQL_PROXY_HOSTNAME=THE_URL_APPLIED_FROM_NGROK_WEBSITE # https://dashboard.ngrok.com/domains
# Ensure under go-svc folder, we run following commands to start the service
TARGET=svc-hr mk aws.migrate.down && TARGET=svc-hr mk aws.migrate.up
TARGET=svc-hr mk compose.up.build AUTH_ENABLED=1
```

### Sub module `svc-hire` setup

- `svc-hire`: is the modules for job listings part of functionality

```bash
# Go to svc-hire/.env file and paste the secrets for the local
cd go-svc
cd nano ./cmd/svc-hire/.env
# Then, paste these credentials into the file: svc-hire/.env
SECRETS_OPENAI_API_KEY=ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_MUX_TOKEN=ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_MUX_TOKEN_ID=ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_MUX_SIGNING_KEY_ID=ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_MUX_SIGNING_KEY_SECRET=ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_SEEK_CLIENT_ID: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_SEEK_CLIENT_SECRET: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_SEEK_AUDIENCE: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_SEEK_GRANT_TYPE: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_SEEK_SCHEME_ID: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_SEEK_WEBHOOK_SECRET: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
APP_CRON_RULE_TENANT_WHITELIST: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_JOB_TARGET_CLIENT_ID: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_JOB_TARGET_CLIENT_SECRET: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
SECRETS_JOB_TARGET_WEBHOOK_SECRET: ASK_TEAM_MEMBERS_TO_GET_THE_SECRETS
# Ensure under go-svc folder, we run following commands to start the service
TARGET=svc-hire mk aws.migrate.down && TARGET=svc-hire mk aws.migrate.up && TARGET=svc-hire mk aws.seed
TARGET=svc-hire mk compose.up.build AUTH_ENABLED=1
# so far, as long as terminal no error reported, svc-hire module has been started successfully ✅
```

### Sub module `svc-query` setup

- `svc-query`: is a service which used for reading the `tenants` database data (powering the graphql API)

```bash
# Ensure under go-svc folder, we run following commands to start the service
TARGET=svc-query mk compose.up.build
# So far, this is the only command we need, and need to confirm with team when having specific requirements 📋
```

### Sub module `svc-url` setup

- `svc-url`: is used for creating `short` urls from the `longer` version of urls for other serices

```bash
# Ensure under go-svc folder, we run following commands to start the service
TARGET=svc-url mk mysql.migrate
TARGET=svc-url AUTH_ENABLED=1 mk compose.up.build
```

### Sub module `svc-dir` setup

- `svc-dir`: is codebase for authenticate the subscription 

```bash
TARGET=svc-url mk aws.migrate.down && TARGET=svc-url mk aws.migrate.up
# TARGET=svc-dir mk aws.seed # Only when needed (Based on the requirements)
TARGET=svc-url mk compose.up.build AUTH_ENABLED=1
```
