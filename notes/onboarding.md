# Onboarding Note

## Setup `deputy-webapp` codebase for local development environment

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
```


## `devbox` codebase setup

About the (devbox github instruction)[https://github.com/DeputyApp/devbox?tab=readme-ov-file#devbox]

```bash
make dns # try to make local site domain url: () load a bit more faster
```

## `go-svc` & sub-services setup

About the (go-sv github instruction)[https://github.com/DeputyApp/go-svc?tab=readme-ov-file#1-clone-the-repo]
