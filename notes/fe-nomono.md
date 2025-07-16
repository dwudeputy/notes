# Micro-frontend (MFE) Codebase setup

## Setup

```bash
# Setup
# clone the codebase as the first step
NOMOMO_REPO=nomono; \
cd $HOME/dev/src/github.com/deputyapp/$NOMOMO_REPO && \
git clone --bare git@github.com:DeputyApp/fe-monorepo.git $NOMOMO_REPO
# install & generate certificates
REPO_FOLDER="fe-monorepo" &&
cd $HOME/dev/src/github.com/deputyapp/$REPO_FOLDER/scripts/local-certs \
&& mkcert -install \
&& mkcert localhost dev.local.dpty.io
# enable the corepack for allow using pnpm without install it
NOMOMO_REPO=nomono; \
cd $HOME/dev/src/github.com/deputyapp/$NOMOMO_REPO && \
corepack enable pnpm
# copy and paste the ngrok url eg: 
{
  "url": "xxx-xxx.ngrok-free.app"
}
# into deputy-webapp `graphql-get-deputy-proxy.json` file in order to start the fe-nomono app
# Start
1. `pnpm i` # at employee-management app/folder directory
2. `pnpm dev:bootstrap` # at fe-nomono root directory
3. `pnpm dev:server` # at fe-nomono root directory to start proxy app dev server
4. `pnpm run dev` # open new terminal at new tab and start `employee-management` app by usual
# 5. replace import map with https://localhost:3030/employee-management/main inside the `Import Map Overrides` UI and click employee-management module
```

<!-- @TODO: will add the missing parts soon -->