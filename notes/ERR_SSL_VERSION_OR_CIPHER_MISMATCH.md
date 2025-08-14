# Error: `net::ERR_SSL_VERSION_OR_CIPHER_MISMATCH` 


## For fixing `deputy-webapp` `vnext` module

Brief: case for trigger this error: The error is occurred when facing importing `main.js` file (module injection) failed,

### How to fix?

Use the command to re-generate the certificates for loading the apps/vnext certificates:

```txt
- Step 1 go to folder: cd frontend/vnext/certs

- Step 2: delete 2 old certificates files if we already created

- Step 3: run command: `mkcert localhost 127.0.0.1 ::1` to generate new certificates

- Step 4: go to folder: cd frontend/vue/certs

- Step 5: delete 2 old certificates files if we already created

- Step 6: run command: `mkcert localhost 127.0.0.1 ::1` to generate new certificates
```

or 

```bash
mkcert -install

# Then inside of certs folder run

cd $HOME/dev/src/github.com/deputyapp/deputy-webapp/frontend/vue/certs/
mkcert localhost 127.0.0.1 ::1

cd $HOME/dev/src/github.com/deputyapp/deputy-webapp/frontend/vnext/certs/
mkcert localhost 127.0.0.1 ::1
```

For the original references:

- Helpful [slack link](https://deputy.slack.com/archives/CNGPL1F7U/p1751441188005089)
- Confluence page [link](https://deputy.atlassian.net/wiki/spaces/FPC/pages/4340711564/VJSM+Using+Vite+for+Local+Dev)


## For `fe-nomono` codebase error fixing

Brief: case for trigger this error: the certs file names are mismatch causes the issue of `net::ERR_SSL_VERSION_OR_CIPHER_MISMATCH`

### How to fix?

The command to generate/re-generate the certificates for WROKTREE localhost server development:

```bash
REPO_FOLDER="fe-monorepo" &&
WORKTREE_FOLDER="main-tree" &&
cd $HOME/dev/src/github.com/deputyapp/$REPO_FOLDER/$WORKTREE_FOLDER/scripts/local-certs/ \
&& mkcert -install \
&& mkcert localhost dev.local.dpty.io
```

The command to generate/re-generate the certificates for NON-WROKTREE localhost server development:

```bash
REPO_FOLDER="fe-monorepo" &&
cd $HOME/dev/src/github.com/deputyapp/$REPO_FOLDER/scripts/local-certs \
&& mkcert -install \
&& mkcert localhost dev.local.dpty.io
```

Ensure to fix the file name must be exactly this name, cannot be localhost`+1`-key.pem:

```bash
- localhost-key.pem
- localhost.pem
```

For the original references:

- Helpful [slack link](https://deputy.slack.com/archives/C075FG0CNKF/p1752643536871439)
- Github page [link](https://github.com/DeputyApp/fe-monorepo/blob/main/_docs/scripts/scripts-local-certs.md#create-ssl-cert-for-localhost-server-development-non-worktree)
