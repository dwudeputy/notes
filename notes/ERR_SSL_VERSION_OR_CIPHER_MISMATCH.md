# Fixing error: `net::ERR_SSL_VERSION_OR_CIPHER_MISMATCH`

Case for trigger this error: The error is occurred when facing importing file failed,

## How to fix

Use the command to re-generate the certificates for loading the apps/vnext certificates:

```txt
- Step 1 go to folder: cd frontend/vnext/certs

- Step 2: delete 2 old certificates files if we already created

- Step 3: run command: `mkcert localhost 127.0.0.1 ::1` to generate new certificates
```

or 

```bash
cd $HOME/dev/src/github.com/deputyapp/deputy-webapp/frontend/vnext/certs/ \
&& mkcert -install \
&& mkcert -key-file 'localhost-key+2.pem' -cert-file 'localhost+2.pem' localhost
```

- Helpful [slack link](https://deputy.slack.com/archives/D095TE54PD0/p1752560985688749)
- Confluence page [link](https://deputy.atlassian.net/wiki/spaces/FPC/pages/4340711564/VJSM+Using+Vite+for+Local+Dev)
