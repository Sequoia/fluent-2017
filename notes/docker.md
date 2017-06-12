## Tests to do
* [x] Run redis locally
* [x] Connect to redis locally
* [x] Use password
* [x] Connect with password
* [ ] Connect from an application

## docker too complicated
* [ ] deploying with persistent storage (not *as* necessary if I only use mlabs)
  * [ ] load mysql dump on startup

## Docker Exercises
* Dockerizing an app
* Running a dockerized app
* Env vars
* Pushing to hub.docker.com
  * Creating account
  * Copy creds --> `docker login`

## Docker networking

*Consider this for linking apps locally*

### Network types
* Bridge: default
* None: none/loopback only
* Host: enables container to attach to hosts network


* docker networking intro: https://runnable.com/docker/basic-docker-networking
* better reverse proxy article: https://www.thepolyglotdeveloper.com/2017/03/nginx-reverse-proxy-containerized-docker-applications/
* worse proxying article: https://linoxide.com/containers/setup-nginx-reverse-proxy-docker/

-----

* [ ] if this doesn't work just bail out & use a remote redis: https://redislabs.com/pricing/redis-cloud/

## Dockerize Node app

https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

## Redis stuff

* https://hub.docker.com/_/redis/
* https://redislabs.com/pricing/redis-cloud/ instead?

### Examples

```Dockerfile
# set port
ENV PORT 80
# overrideable by passing --env FOO='abc 123' to `docker run`
ENV FOO "--------bar----------"

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . /usr/src/app

# replace this with your application's default port
EXPOSE $PORT

CMD [ "sh", "-c", "npm start -- $FOO" ]
```

### [example](https://github.com/spkane/hubot-docker/blob/master/Dockerfile)
```Dockerfile
FROM node:5.7.1

RUN mkdir -p /data/app/bin && mkdir -p /data/app/scripts

RUN apt-get -y update
RUN apt-get -y install supervisor python-pip
RUN easy_install -U pip
RUN pip install supervisor-stdout
RUN mkdir -p /var/log/supervisor

# Supervisor Configuration
ADD ./supervisord/conf.d/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD ./supervisord/conf.d/hubot.conf /etc/supervisor/conf.d/hubot.conf

ADD ./bin /data/app/bin
ADD ./scripts /data/app/scripts
ADD ./*.json /data/app/

RUN cd /data/app && npm install

CMD ["supervisord", "-n"]

```

# Set up

This guide is from https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

## Building

```
$ docker build --tag <your username>/node-web-app .
```

## Running

```
$ docker run -p 49160:8080 --name name-the-instance -d <your username>/node-web-app
```

Check it's up
```
docker ps
CONTAINER ID        IMAGE                       COMMAND             CREATED             STATUS              PORTS                     NAMES
49d90a8bb8f6        sequoia/node-hello-docker   "npm start"         4 seconds ago       Up 3 seconds        0.0.0.0:49160->8080/tcp   hello-docker
```

Hit it from host:

```
$ curl -i localhost:49160
```

## Utility

```
## Print the output of your app:

# Get container ID
$ docker ps

# Print app output
$ docker logs <container id>

# Example
Running on http://localhost:8080

## If you need to go inside the container you can use the exec command:

# Enter the container
$ docker exec -it <container id> /bin/bash

## To test your app, get the port of your app that Docker mapped:

$ docker ps
```