# Portainer

## Table of contents
* Prerequisites
* Overview
* Prepare the `.evn`file
* Start Portainer via `docker-compose`

## Prerequisites
Install `Docker` and `docker-compose`

## Overview

```bash
$HOME/docker/portainer/
├── docker-compose.yml
├── .env
└── .env-sample
```

## Prepare the `.env' file

```bash
cd ~/docker/portainer
cp .env-sample .env
nano .env
```

Replace data with your own configuration:

```bash
COMPOSE_PROJECT_NAME=portainer
TIMEZONE=Europe/Berlin

#CHANGE_BEFORE_FLIGHT
IP_ADDRESS=#YOUR_IP
SHARE_PATH=#YOUR_PATH
```

## Start Portainer via `docker-compose`

With all configuration done you can start the Portainer container:

```bash
cd ~/docker/portainer
docker-compose up -d
```

To check if everything is running fine you can run `docker ps` and look for a container named `portainer`.