# Updated version for Dev Setup document 

This note is mainly focus on updating the obslete part of document from the original [dev-setup document](https://engineering.mgt.dpty.io/dev-setup.html).

## Update version on 17/07/2025

### For `Dev Setup` Section


1. About the [docker](https://engineering.mgt.dpty.io/dev-setup.html#docker) setup guide,

Please ensure we are currently need to install version `27.5.1`, here is the (link)[https://docs.docker.com/desktop/release-notes/#4380] for Mac & Windows OS.

2. About the [nvm](https://engineering.mgt.dpty.io/dev-setup.html#nvm) installation, please also ensure the node version must be `v18.16.0`

How to install?

```bash
nvm install v18.16.0
nvm use v18.16.0
nvm alias default v18.16.0
```

### For `System Setup` Section

1. For the section of (Installs)[http://engineering.mgt.dpty.io/systems-setup.html#installs], as a frontend engineer, currently its not required to install these libs (Can be ignored for now).

2. For the (Github setup)[https://engineering.mgt.dpty.io/systems-setup.html#github-setup] section, please ensure fowllowing keys are added:

```bash
- GPG Key
- SSH Key
```
<!-- Can make validation for 1 year -->

![Github GPG Key](./assets/github-gpg-key.png)

![Github SSH Key](./assets/github-ssh-key.png)

Also ensure authorize the `DeputyAPP`

![Github GPG Key](./assets/deputy-authorize.png)


* So far, thats all the changes we can follow this updated note instead of original dev-setup document, but for the rest of the configurations, it would be reommanded to follow the original dev-setup document.
