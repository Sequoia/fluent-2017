# Stuff to cover

## Day 1
Total time herein: 6.5hrs (.5hrs over)
* msvs concepts: .5hrs
  * general architecture
  * pros and cons
    * pitfalss
  * different approaches
    * platforms / ecosystems
    * containerization
    * 3rd party services
  * containers
    * Docker
    * Docker-compose
    * Docker-swarm
    * redis
* lambda: 3hrs
  * PHASE I: 2hrs
    * setup
    * running directly on aws
    * output : sns/email
    * input : exposing via HTTP
    * Serving files from S3
  * PHASE II (later, after some `now` stuff?): 1hr
    * running locally: node-lambda
    * config/env vars:
      * s3config
      * node-lambda
    * node scripts w/node-lambda
* APIC: 1hrs (keep this sorta short)
  * What is bluemix
  * Setting up an API with apic CLI
  * Running locally
  * API composer
  * Deploying to bluemix
  * Relationships? (TA)
  * Testing with postman
* Authentication: JWTs: 1hr
  * What are they
  * When to use them
  * Pitfalls of replacing sessions with JWTs
  * Validating requests on lambda with JWT
* Authentication: sessions: 1hr
  * sharing sessions across microservices
  * redis
  * mongo/mongolabs
  * running locally

## Day 2
Total time herein: 6 (or more :p)

* Authenication wrap-up: .5hr
* Now: 2hrs?
  * Deploying to now
  * Static deploys
  * Node.js deploy
    * micro
    * express
  * Scaling
    * Scaling an app up & down
  * External settings
    * Env switch
    * Env files
    * Secrets
    * Connecting to mlabs e.g.
  * Aliasing
    * simple alias
    * alias rules
    * grouping applications via alias
    * external passthrough
    * Integrate lambda
* Docker: 1.5hrs
  * Docker intro
  * Benefits & Limitations
  * Dockerizing redis
    * Configuring password (externally)
    * Exposing a port
    * ENV vars
  * Dockerizing a node app
    * Accessing locally
    * SSHing to docker
    * Deploying to now
  * Reconfiguring app to work with local redis
  * Running locally with docker-compose
    * links
* Kubernetes: 1.5hrs
  * PHASE I: Explainer: .5hr
    * What is it
    * Different components
    * Where it fits with Docker
    * Benefits
    * labels & selectors
  * PHASE II: Hands on: 1hr
  * minikube
    * configuration
    * kubectl
      * tons of commands to looka t
  * cluster
  * pods
  * services
  * deployments
  * configuring pods, services, etc.
  * creating instances on kubernetes
  * dashboard!
  * converting docker app to kubernetes deployment
* GKE: .5hrs
  * Setting up GKE
  * deploying app to GKE
  * dash