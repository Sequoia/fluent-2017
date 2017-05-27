## Tests to do
* [x] Run redis locally
* [x] Connect to redis locally
* [x] Use password
* [x] Connect with password
* [ ] Connect from an application

## docker too complicated
* [ ] deploying with persistent storage (not *as* necessary if I only use mlabs)
  * [ ] load mysql dump on startup

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