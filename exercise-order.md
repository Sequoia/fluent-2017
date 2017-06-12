Main exercises will revolve around decomposing our application, with side-exercises to explore platforms and tools

1. Setting up & running monolith application `01-Monolith`
    * 483c93bbe4be85fb0a990554007b5bc9bf8de341
    * Starting point: monolith application
2. Deploying to now `02-Now` ()
    * externalize configuration
    * `-e` `--dotenv` `package.json.now.env`
    * secrets
    * try scaling (see it doesn't work)
    * `02-Now-done`
3. Creating books microservice with APIC `03-APIC`
    * Register for IBM Bluemix
        * Create an "org"
        * Create a "space" (`dev`);
    * Install tools: `apiconnect`
    * Generate application: `apic loobback`
    * Configure server: 
    * `03-APIC-done`
4. Customizing our loopback API
    * api path: `/`
    * relations
    * scope
    * remote method
    * Do this one (*step by step*) and let attendees copy
    * Extra credit
        * Create relationships from Languages & Authors back to books
        * Create environment specific configs

5. Updating books service to point to external API
    * Update Service to use promises (together)
    * Update payments route (together)
    * Update books router (attendees)
    * Run it locally

6. Deploying Books API to now
   1. Now: Some basic exercises TODO
      * Deploy
      * scaling
      * Alias
      * Alias rules
      * setting env vars
      * now logs
      * https://zeit.zeit.ninja/dashboard
   2. Deploying our updated books API application to `now`
      * Externalizing credentials:
        * BOOKS_DB
      * Deploy (w/env vars)
      * Aliasing Books DB now instance

7.  Deploying updated Monolith to `now`
    1. Edit & Deploy
        * Externalizing BOOKS_API (point to `my-books-api.now.sh`)
        * Deploy (w/env vars)
        * Alias monolith `<yourname>-monolith.now.sh`
        * Passthrough "/Books**"
    2. Remove books router
        * Deploy
        * Update aliases
        * See that it works
    3. Show them the other possible way to alias
        * `BOOKS_API` points to `yourname-monolith.now.sh/Books`
        * Now you can swap out `yourname-books-api.now.sh` without `monolith` knowing about it

8.  Deploying Books API to bluemix
    * set up app/product/catalog
    * deploy
    * set env vars there
    * pick alias name
    * See that it works
    * add bluemix alias to now-alias for monolith
        * update alias on `now`
        * remove books service on now


5. Deploy
   * APIC: you must first go here and create a service: https://console.ng.bluemix.net/dashboard/apps/
   * Add a new aliased route