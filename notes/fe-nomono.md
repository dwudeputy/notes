# Micro-frontend (MFE) Codebase setup

## Setup commands

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
# please ensure your secret files must be named EXACTLY as under the path: 
- localhost-key.pem
- localhost.pem
# enable the corepack for allow using pnpm without install it
NOMOMO_REPO=nomono; \
cd $HOME/dev/src/github.com/deputyapp/$NOMOMO_REPO && \
corepack enable pnpm
# copy and paste the ngrok url into deputy-webapp project file named as `graphql-get-deputy-proxy.json` eg: 
{
  "url": "xxx-xxx.ngrok-free.app"
}
# into deputy-webapp `graphql-get-deputy-proxy.json` file in order to start the fe-nomono app
# If haven't run the ngrok command, please run: ngrok http --url=xxx-xxx-xxx.ngrok-free.app 8888 # (eg: ngrok http --url=internally-quick-boxer.ngrok-free.app 
# please ensure copy the "url": "xxx-xxx.ngrok-free.app" into deputy-webapp project

# Start
1. `pnpm i` # Install dependencies at the root of the app directory (`apps/employee-management`)
2. `pnpm dev:bootstrap` # Install dependencies from the `root` folder
3. `pnpm dev:server` # at fe-nomono root directory to start proxy app dev server
4. `pnpm run dev` # open new terminal at new tab and start `employee-management` app by usual
# 5. replace import map with https://localhost:3030/employee-management/main inside the `Import Map Overrides` UI and click employee-management module
```

For more general app running and development info, please have a look at these documents:

The original Dev Server configuration reference: [scripts-migrate-shared-vite-config.md](https://github.com/DeputyApp/fe-monorepo/blob/main/_docs/scripts/scripts-migrate-shared-vite-config.md)
The original App configuration reference: [apps-development.md](https://github.com/DeputyApp/fe-monorepo/blob/main/_docs/apps/apps-development.md)
