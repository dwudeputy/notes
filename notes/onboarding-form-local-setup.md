# Onboarding Form Local Setup

Before trying to work on AU/UK/US onboarding form local setup, lets follow the below steps, to setup 3 environments (AU/UK/US) for the feature code development

## How to test 3 environments (AU/UK/US) for the feature code development

- Run `make upd` at deputy-webapp terminal (restart container) [Also, sometimes, need to restart docker cobtainer and then seed again, sometimes not working properly after few rounds of testings]
- Run `make seed.e2e` at deputy-webapp terminal (start e2e seed mode)
- Run `make fe.dev` at deputy-webapp terminal (runn app)
Open link: `https://once.local.dpty.io` link and ensure VPN + Deputy Cafe (localhost) is on as usual
(Soem times, need to re-run `make dns` under devbox codebase to restart the dns)
Type `dev.deputec.com` + `password` for login

Thats it, now we are able to view the 3 environments test instances for local dev environment. Next step is to choose one of region url and start to generate onboarding link and in order to fill onboarding data.


## For AU setups

Step 1: Always turn on `web-hr` by `npm run dev`

Step 2: Go to `svc-hr` README file, run this command: `cmd/svc-hr/vault.migrate.sh up` in terminal for support s3 file upload in local environment

Step 3: Now, `onboarding new hire` and fill the form data and `onboard team member`, after trigger API call, will get the link from API response, like below:
![Example AI Response](./assets/images/PWF-7122-local-onboarding-link.png)

Step 4: When we copy the link from `onboarding` API response, eg: `https://api.local.dpty.io/u/31VNJxCssNEyietCKev56AP2O06`

Step 5: We just opened it in a browser tab, then we will get yne token based new link, and then we just need to change that token based new link (eg: `https://webdev.local.dpty.io/#/onboarding/31VNJubQSEABhIOk3DmKHwsb8qJ;eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJhcGkuZGVwdXR5LmNvbS91cmwvdjEiLCJleHAiOjE3NTU2NDk5MDIsImlhdCI6MTc1NTY0OTYwMiwiaXNzIjoiYXBpLmRlcHV0eS5jb20vdXJsL3YxIiwianRpIjoiMzFXcElRNnpuVTlaNEtFUmtYelVUOXBQNlVRIiwibmJmIjoxNzU1NjQ5NjAyLCJzdWIiOiJhcGkuZGVwdXR5LmNvbS91cmwvdjEvc2hvcnQtdXJscy8zMVZOSnlTb3NsSm5pMzh4WXJJU2l4WllrbmsifQ.PZd8e7-BT0C2LvS4dFkWvXshvZaXwkEcYpWjJmR4gKf97GLkqhIgfUJpdaB36ARdF_mjtW3EDob3STpAuis2Sg`) replace `https://webdev.local.dpty.io` with `localhost:8888 or 8889` to open the local onboarding form link

One of workable examples: `http://localhost:8888/#/onboarding/31dw8Rc2ao3DNczowt8oVJ5v21V;eyJhbGciOiJIUzUxMiIs[…]7BlyPTSY_V5JNi77RgFi3HbVhVhGlXpA1G1LltX_sJnlrG_m7lhXpOPS-VDeg`

## For US setups

Same to follow above all AU steps.

Meanwhile, the special part for US setup is `form.io` (ONLY US using form.io), which needs 2 steps:

Additional step 1: 

We need to create `tenant` for US via Postman, when doing US onboarding form local development, here is the `POST` API request body payload:

```json
{
    "data": {
        "id": "af4d2bb2-1d28-11ed-861d-0242ac120002",
        "hostname": "usbusiness.dev.local.dpty.io",
        "additionalHostname": "usbusiness.dev.local.dpty.io",
        "portfolioName": "Deputy Development US",
        "countryCode": "US",
        "countryId": 223,
        "region": "usw2",
        "creator": "-2",
        "status": "ACTIVE",
        "edition": 11,
        "enabled": true,
        "channel": "DIRECT",
        "billingSuppressed": false,
        "trialEndedAt": null,
        "conversionDate": null,
        "dbHost": "svc.db.local.dpty.io",
        "dbName": "deputec_dev",
        "dbUser": "",
        "redisTenantCluster": "redis-tenant.local.deputec.com:17000",
        "elasticsearchHost": "",
        "subscriptionMetadata": {},
        "createdAt": "2019-05-22T15:34:47Z",
        "modifiedAt": "2023-06-05T12:29:37Z",
        "externalId": "",
        "addOnProducts": {
            "hr-suite-standard": {
                "name": "Deputy HR",
                "identifier": "hr-suite-standard",
                "trialDays": 31,
                "trialStartDate": "2023-07-22T15:34:47Z",
                "trialEndDate": "2024-07-23T15:34:47Z",
                "trialAvailable": true,
                "terminationDate": "2024-02-10T15:34:47Z",
                "status": "ACTIVE",
                "createdBy": "1"
            }
        }
    }
}
```

Additional step 2: fill in all necessary secrets under svc-hr repo:

```txt
APP_DEPUTY_GRAPHQL_PROXY_JWT_KEY=GET_VALUE_FROM_ONE_PASSOWRD_SVC_HR_FILE
APP_DEPUTY_GRAPHQL_PROXY_HOSTNAME=OWN_NGROK_URL
APP_MIGRATION_SHOULD_USE_NEW_ONBOARDING_STRUCTURE=GET_VALUE_FROM_ONE_PASSOWRD_SVC_HR_FILE 
APP_HELLOSIGN_DEFAULT_TIMEOUT_IN_SECONDS=GET_VALUE_FROM_ONE_PASSOWRD_SVC_HR_FILE
APP_FORMIO_PROJECT_URL=GET_VALUE_FROM_ONE_PASSOWRD_SVC_HR_FILE
APP_FORMIO_PROJECT_PATH=GET_VALUE_FROM_ONE_PASSOWRD_SVC_HR_FILE
SECRETS_FORMIO_API_KEY=GET_VALUE_FROM_ONE_PASSOWRD_SVC_HR_FILE
```

## For UK setups

Same to follow above all AU steps.
