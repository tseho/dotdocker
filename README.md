# dotdocker

**Please do not use it in production.**

It's a docker/docker-compose config for Symfony (^3.4 || ^4.0), nginx and mariadb.

## Installation

In your Symfony installation, run the following commands:
```
git clone --depth=1 --branch=master git@github.com:tseho/dotdocker.git .docker
cd .docker && rm -rf .git
./configure
```
Once installed, you can then start the containers with docker-compose when inside the **.docker** directory:
```
docker-compose up -d
```

## PostgreSQL

You can easily replace mariadb by PostgreSQL, if needed, with small changes in the following files:
- docker-compose.yml
- .templates/docker-compose.override.osx.yml
- .templates/docker-compose.override.unix.yml
- app/Dockerfile
