# Examples

## Setup

vi Dockerfile
```
FROM ruby:alpine3.15

WORKDIR /usr/src/app/

RUN apk --update add --no-cache --virtual run-dependencies \
        terraform \
        aws-cli

RUN gem install terraforming
```

Build image
```
docker build -t terraforming:1.0 .
```

Run Image
```
docker run -it terraforming:1.0 sh
```






