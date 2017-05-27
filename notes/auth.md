# Goals

* [X] ~~*Auth server, auth against mongodb*~~
* [X] ~~*Redis to track sessions?*~~
* [ ] Generate tokens for Lambda
* [ ] Read tokens on Lambda

## Auth Server

## Versions/phases

### Mongoose
1. Setup mongoose user model
  * Check connection & saving/retrieving
2. Add set password to mongoose user
  * Check
3. Add check password method
  * Check

### Passport
0. In memory session, in memory user, in memory serialize
1. Local strategy: check against in-memory u/p
2. Local strategy: Check against Mongoose user

### Redis
0. In memory session
1. Check redis connection
2. SESSION in redis
  * See that it works
  * Quit browser & see that it works
  * Restart server and see it *doesn't* work (Not fully stateless! Only session is stateless, not serialization strategy)
3. SERIALIZED USER in redis
  * See it works
  * Restart server & see that it works
  * Serializing user:
    * `user.toJSON()` This is an object not a JSON string!!
    * `user.toString()` This includes _id 

## Routes & steps

Express for ease

* [X] ~~*/login*~~
* [X] ~~*/logout --> redis*~~
* ~~[ ] */register*~~ skip this
* [X] ~~*Externalize mongo url*~~
* [X] ~~*Externalize redis url*~~
* [ ] Alias on `now`: /auth/

## ~~Redis session tracking~~

* [X] ~~*Redis docker container*~~ <-- replace with redislabs
* [X] ~~*Expose ports*~~
* [X] ~~*Check session*~~
* [X] ~~*Set/create session*~~
* [X] ~~*Destroy session*~~
* [X] ~~*Alias on `now`*~~

* [X] ~~*Create app server (product-server)*~~
* [X] ~~*Run locally on two ports*~~
  * **Works!!**
* [X] ~~*Have it pass through auth*~~
* [X] ~~*Have it access redis session created by auth server*~~

## Externalize auth/checking stuff

* `loggedIn`
  * Stateless/encapsulated
  * Used by both
* mongo Strategy
  * relies on mongo
  * Used by AUTH only
* serialize/deserialize user
  * relies on redis
  * Used by BOTH
  * *if I change this to deserialize from mongo it will also require mongo*
  * *if I put the entire user object into the serialized version, I will only need to access redis from the session portion* --> Simpler

* [ ] SPLIT THIS UP and EXTERNALIZE to a 3rd package so each module can require just the bits it needs
  * (Time allowing i.e. do this later)
