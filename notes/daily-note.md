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