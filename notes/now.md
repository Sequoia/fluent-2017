**Now & Micro notes**

# Now

## Setup
1. Install client: [guide](https://zeit.co/docs/getting-started/installing-now#the-app)
  * Desktop client https://zeit.co/download
    Then click icon &rarr; about &rarr; tutorial &rarr; step 3: install CLI
  * *CLI only*: `npm i -g now`
2. `now login`
3. Check email & verify address
   Token now in `~/.now.json`

## Deploying

### Static site deploy
1. Create index.html
2. Deploy

### Node project deploy
0. Create new project (`npm init -y`)
1. Create an `index.js` file
1. Set `scripts.start` to `node index.js`
1. Test locally: `npm start`
2. `now`

## Viewing source
* `/_src`
* Disabling view src

## Customizing Deploy
* Node version:
  * `engines.node`
  * `now.engines.node`
* build step:
  * `scripts.build`
  * `scripts['now-build']`

## Secrets & Env vars

*Keep a text file of your secret keys/urls on hand somewhere during these exercises!*

### Env vars:
1. `-e foo=bar`
2. `--dotenv`
  * reads from `.env`
  * **`.env` IS NOT HIDDEN FROM `/_src`!** Use secrets:
3. `package.json` for *fixed* env values
  ```js
  ...
    "now" : {
      "env" : {
        "DATABASE_NAME" : "test"
      }
    }
  ...
  ```
4. `now.json` for non-node projects (i.e. docker)
  * made available to docker `RUN` & `CMD` commands


### Secrets
* create: `now secrets add my-secret "secret value"`
* use:
  * `-e MONGOURI=@my-secret`
  * `.env`
    ```
    MONGOURI=@mysecret
    ```
    Deploy with `--dotenv`


* Added env vars:
  * `NOW_URL` env var scripts can use
  * `NOW` for detecting that it's `NOW`


## Aliasing
1. Create an alias for a single service
2. Create an alias for another service
3. Create alias rules to proxy a path through to another service
4. Create an alias rule to proxy to an *external* service (lambda e.g.)

## Scaling
1. Create counter server (pid, count)
2. Scale others 0
3. Scale 3
4. See counts

`now scale ls`
`--debug`

### Autoscaling

:( Not available at pro level
1. Set scale rules min/max
2. Generate load
3. See scaled

## External domain (PAID ACCOUNTS ONLY)
*probably just demo this stuff, not exercises*
* https://zeit.co/docs/features/zero-downtime-migration
* https://zeit.co/docs/features/dns

## Questions
* [ ] Teams? Worth setting this up?
* [x] How easy is deploying dockerized app? --> easy
* [x] hidden keys/tokens etc.? Deploy these?
  &rarr; use `-e MONGOURI=xyz`
  &rarr; use `now secrets` to set secrets then `-e MONGOURI=@mongo1`

## More Info
* Pricing: https://zeit.co/pricing
  Looks like you get 3 concurrent instances for free
* Now platform advantages: https://zeit.co/now#frequently-asked-questions
  Also: https://zeit.co/docs/getting-started/introduction-to-now#how-is-it-different
* Nice guides: https://zeit.co/docs
* "When an instance restarts for any reason (or exit code), we automatically restart the instance, so supervisor-like wrappers are not necessary. For example forever, nodemon or pm are not necessary for an application to always stay running."
* "**Not for databases** because deployments are immutable" - `now` guy.