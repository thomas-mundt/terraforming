# Examples

## Setup

vi Dockerfile
```
FROM ruby:alpine3.15

WORKDIR /usr/src/app/
ENV AWS_REGION=eu-central-1

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


Installed Tools in image
- terraform
- terraforming
- aws


## Usage

Show help
```
terraforming
```







