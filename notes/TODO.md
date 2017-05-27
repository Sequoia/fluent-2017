* [ ] dockerizing nginx app
* [ ] ->  with filesystem
* [ ] dockerizing loopback app
* [ ] dockerizing mysql server (with data)
  * http://blog.turret.io/a-better-dockerized-mysql/
  * http://www.nkode.io/2014/09/12/easymysql.html
* [ ] dockerizing “micro” or “next” web server thing
* [ ] posting these container images somewhere (“repository”)
* [ ] managing env/secrets
* [ ] running locally
* [ ] Tying these together with kubernetes
* [ ] Running kubernetes locally
* [ ] Deploying to GKE
* [ ] Getting data into kubernetes/docker things

# Setup

## Micro + Now

* ~~[ ] micro app scaffolding~~
* [x] Deploy to Now
* [x] List deployments
* [x] Aliasing
* [x] have it do something
* [ ] have it access some 3rd party thing
* [x] update & deploy
* [ ] Test micro app
* [ ] dockerize micro app
* [x] deploy dockerized app to now! ?

## Next

**Constrain this exercise!! If it gets too crazy cut it**

**Can't spend too long on this in lesson! Not a msv thing strictly speaking: consider simpler option if it takes too long**

* [ ] Create simple "next" app
* [ ] Load some data from client
* [ ] Load some data from startup
* [ ] Dockerize
* [ ] Have dockerized version interact with another docker container (get data e.g.)

## MySQL
* [ ] Create docker image
* [ ] Startup file that loads data

## LoopBack
* [ ] Product DB
* [ ] Cart DB
* [ ] Dockerize?
* [ ] Ship to BlueMix
* [ ] Access data from another docker container/server

## Algolia
* [ ] Setup
* [ ] Test search API
* [ ] Build it into an app

## Lambda
* [ ] Create a lambda to process orders
* [ ] Have it add order to a queue
* [ ] Send an email
* [ ] Security/tokens?
* [ ] AWS CLI? http://docs.aws.amazon.com/lambda/latest/dg/with-scheduled-events.html

## Docker
* [ ] Deploying to registry
* [ ] Loading apps from registry

## Authentication
* [ ] jwt?
* [ ] Login system for web application
* [ ] Users microservice?

## Apigee
* [ ] Watch tutorial video
* [ ] Describe how it will fit in

## Auth0

Very easy to set up.
Try it with JWT? &rarr; Looks to be a good bit more complex. Try if time & algolia doesn't come through.


* [X] ~~*Try basics*~~
* [ ] Try it with JWT

# Application Features


# More stuff?

* https://www.draw.io/

Jesse Kochis
the basics that I've learned so far:
11 minutes ago
J
Jesse Kochis
hovering over an object on your stage does three things depending on where you cursor is:
11 minutes ago
J
Jesse Kochis
little 'x'es are anchor points that turn green when you hover over one
10 minutes ago
J
Jesse Kochis
click and drag to create an arrow
10 minutes ago
J
Jesse Kochis
you can drag it to another anchor point that appears when you get close to another object
9 minutes ago
J
Jesse Kochis
pale blue triangles: click to quick add a new object with an arrow between it and the current one
8 minutes ago
J
Jesse Kochis
that's the basics to building out a diagram real fast
7 minutes ago
J
Jesse Kochis
then you can worry about sizing and arranging after you've got your thoughts on paper
7 minutes ago
J
Jesse Kochis
visio would mess me up with how it would try to do smart stuff while I was just trying to get my thoughts out
6 minutes ago
J
Jesse Kochis
also, our dev process has been pretty agile WRT lots of tech and shifting changes, and this is really easy to update without needing to start over