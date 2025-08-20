# Daily Note

- The note is more like daily knowledge insertion, better reach to myself for explanantion if not clear on some quick notes (Happy to explain) ~

- This note is focus on writing the some essential notes for daily works

## `prodtest` setup

Here are the steps:

> 1. Go to Github, and select the label of `prodtest server` from labels area in the PR
> 2. Always remember to wait for `artefact-ready` to show then start to do the prodtest (Normally wait for 10 -15 mins)
> 3. Setup Deputy Cafe `dns` address with auto generated the message from github PR.
>    Like image shown below
![GET ProdTest DNS Address](assets/images/pr-dns.png)
> Then, `add` dns into `Deputy Cafe` app
![Add ProdTest DNS Address](assets/images/add-prodtest-dns.png)
> 4. (ONLY ask once) Also need to ask team members to invite and click 'Accept' to join the `coconut prodtst` app to start to do the prodtest !!
> 5. Do a loom video record and attach it to Github comment area


## Never change `coconutprodtest.au.deputy.com` url to your own URL, (PLEASE REMEMEBR 📝)

For checking with all permissions setup: please add this `exec/administration/workforce/employee_roles` after `https://coconutprodtest.au.deputy.com/#/`

Example: [https://coconutprodtest.au.deputy.com/#/exec/administration/workforce/employee_roles](https://coconutprodtest.au.deputy.com/#/exec/administration/workforce/employee_roles)


## `hello sign` setup

Reference [doc](https://deputy.atlassian.net/wiki/spaces/hr/pages/2522415137/Set+up+dropbox+sign+local+environment)

Local setup steps:

```bash
# To Be Described
```


## For checking the leagacy CUE tickets, if no dieas, please check with following steps:

- Always check with [help doc](https://help.deputy.com/hc/en-au/categories/7657951512591-Deputy-HR-AU-UK-US), if related with other teams, can check with this [url](https://help.deputy.com/hc/en-au) too

- Do a confluence doc search based on `keywords`

- Check with `Slack` chat history


## For `web-hr` local setup

Can just follow the [README](https://github.com/DeputyApp/web-hr/blob/main/README.md) file, run this command

```bash
npm run dev
```

to start local, thats it, nohing more so far.


## For `Kudos` local setup

Kudos requires `svc-dir` + `svc-cultre` modules to be up and running, here is the update notes for the original [documentation](https://deputy.atlassian.net/wiki/spaces/hr/pages/4658594008/Run+Kudos+in+Local)

Changes are:

1. Run this command `TARGET=svc-dir mk aws.migrate.down && TARGET=svc-dir mk aws.migrate.up` first, then run `TARGET=svc-dir AUTH_ENABLED=false mk compose.up.build`

2. Before run step 3, please ensure Deputy Cafe need to run `localhost:127.0.0.1`


## The HR team bible

The [HR bible](https://help.deputy.com/hc/en-au/articles/4658199944847-Deputy-access-levels?gad_source=1&gad_campaignid=22731064046&gbraid=0AAAAADBqLlDJfWbTKm9matIfr2DAlrfhx&gclid=Cj0KCQjwnJfEBhCzARIsAIMtfKJzXQPTgFapDWI_sglWLCF3jIZNwo_-nLZsWEDf5JTjBYHKnBs145waAutAEALw_wcB)

Please read it if you are part of HR team ~

## How to run unit tests at `vnext` deputy-webapp project

```bash
# RUN for specific (eg: Module) folder
npm run test:unit -- --testPathPattern="modules/integrations"
# RUN a specific unit test based on path pattern
npm run test:unit -- --testPathPattern="bank-details-conditional-value.spec.ts"
# RUN a specific unit test (single file)
pnpm test:unit src/tests/lib/feature-gating.spec.ts --run
```

## `Preferences` APIs:

This is the API endpoints which uses for saving some values into local stroage, it has prefix value: `API_PREF`

```bash
# For Prodtest Environment:
https://coconuttestchangeurl.au.deputy.com/api/management/v2/employee/279/preferences
# For Local Environment:
https://business.dev.local.dpty.io/api/management/v2/employee/1/preferences
```

Also in browser, we could use this command to trigger API request and then manual control the preference values inside localstorage, by typing:

```bash
# { syncBackend: true }: means it will sync with backend
# Pleas ensure the variable name must be WITHOUT API_PREF prefix, just the variable name ONLY ~
window.globalLibs.PreferencesV2Service.updatePreference('VARIABLE_NAME_WITHOUT_API_PREF_PREFIX', value, { syncBackend: true })
# window.globalLibs.PreferencesV2Service.updatePreference('KudosWelcomeBannerHidden', false, { syncBackend: true })
```

Reference [doc](https://deputy.atlassian.net/wiki/spaces/FPC/pages/2505146395/Webapp+User+Preferences) from confluence


## How to fix localhost DNS not able to connect issue

![Wifi icon always shows the RED colour](assets/images/localhost-dns-failed-to-connect.png)

Conclusion: No good way found so far, has to turn oof all docker containers and restart laptop, and restart all related services and APIs we needed

Other devs tries - reference: [slack chat](https://deputy.slack.com/archives/C04CTF1HF9D/p1741906810669149?thread_ts=1741863392.508929&cid=C04CTF1HF9D)

## `PRF_653` FF has been removed (Feature Gating Plan)

In terms of `PRF_653` FF get deleted, the replacement solution is to (PWF-6997 related):

- Using postman to update edition to `40` from `1`
![Postman update the Edition value](./assets//images/PRF_653.png)
- Using `SettingConstants::PEOPLE_TAB_PEOPLE_CUSTOM_FIELDS_LINK => Features::FOUNDATIONS_SHIFT_CUSTOM_FIELDS`, inside `Tenant/Domain/BusinessSetting/Service/FeatureGating/FeatureGateSettingVisibilityMapper.php` file

This is how to trigger local testing ~

The Feature Gating Plan Definition: [link](https://deputy.atlassian.net/wiki/spaces/GROW/pages/4662034532/Feature+Gating+by+Plans+and+Add-ons)


## About the local onboarding dev setup (Issues faced)

About local onboarding dev setup: [link](https://deputy.atlassian.net/wiki/spaces/hr/pages/404949111/Employee+Onboarding+DEV+setup)

Please follow this thread for more info: [link](https://deputy.slack.com/archives/C075FG0CNKF/p1755576394139399)

Please remember suggestion form team member:

That's the CORS issue with `svc-hr` as it now only allows request from port 8888.

Albert's solution works for onboarding only.

If you still need to turn on ngrok, then open `svc-hr/data/config/app.yaml`, search for `"localhost:8888"` and replace with `"localhost:8889"`, then run `TARGET=svc-hr mk data & TARGET=svc-hr mk compose.upbd` ~

PLEASE PLEASE FOLLOW THIS INSTRUCTIONS !!!!!!!!!!!!!!! (IMPORTANT ONE)
This is the correction for the original documentation.

(1). When we copy the link from `onboarding` API response, eg: `https://api.local.dpty.io/u/31VNJxCssNEyietCKev56AP2O06`
![]()
(2). We just opened it, then we will get yne token based new link, and then we just need to change that token based new link (eg: `https://webdev.local.dpty.io/#/onboarding/31VNJubQSEABhIOk3DmKHwsb8qJ;eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJhcGkuZGVwdXR5LmNvbS91cmwvdjEiLCJleHAiOjE3NTU2NDk5MDIsImlhdCI6MTc1NTY0OTYwMiwiaXNzIjoiYXBpLmRlcHV0eS5jb20vdXJsL3YxIiwianRpIjoiMzFXcElRNnpuVTlaNEtFUmtYelVUOXBQNlVRIiwibmJmIjoxNzU1NjQ5NjAyLCJzdWIiOiJhcGkuZGVwdXR5LmNvbS91cmwvdjEvc2hvcnQtdXJscy8zMVZOSnlTb3NsSm5pMzh4WXJJU2l4WllrbmsifQ.PZd8e7-BT0C2LvS4dFkWvXshvZaXwkEcYpWjJmR4gKf97GLkqhIgfUJpdaB36ARdF_mjtW3EDob3STpAuis2Sg`) replace `https://webdev.local.dpty.io` with `localhost:8888 or 8889` to open the local onboarding form link
```


## How to test 3 environments (AU/UK/US) for the feature code development

- Run `make seed.e2e` at deputy-webapp terminal
- Run `make fe.dev` at deputy-webapp terminal
Open link: `once.local.dpty.io` link and ensure VPN + Deputy Cafe (localhost) is on as usual
Type `dev.deputec.com` + `password` for login

Thats it, now we are able to view the 3 environments test instances for local dev environment
