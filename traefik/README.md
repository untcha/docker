# _Traefik

# Preparation

## Overview

```bash
$HOME/docker/traefik/
├── auth
│   └── .htpasswd
├── config
│   ├── dynamic.yml
│   ├── rules.yaml
│   └── traefik.toml
├── docker-compose.yml
├── .env
└── letsencrypt
    └── acme.json
```

## Create docker network

```bash
docker network create traefik_proxy
```

## `Basic Auth` for the Dashboard
It is recommended to enable `Basic Auth` when using the Traefik Dashboard. This will be enabled by using this `docker-compose` `label`:

```yaml
labels:
  - "traefik.http.middlewares.auth.basicauth.usersfile=/auth/.htpasswd"
```

To create the user and password combination the `apache2-utils` package is required:

```bash
sudo apt install apache2-utils -y
```

Then create the `.htpasswd` inside the `auth` folder:

```bash
cd auth
mv .htpasswd-sample .htpasswd
# don't forget to replace brackets < >!
echo $(htpasswd -nbB <USER> "<PASS>") > .htpasswd
```

Alternative:

```yaml
labels:
  - "traefik.http.middlewares.auth.basicauth.users=${HTTP_USERNAME}:${HTTP_PASSWORD}"
```

In this case the `$` signs need to be escaped in the password:

```bash
# don't forget to replace brackets < >!
echo $(htpasswd -nbB <USER> "<PASS>") | sed -e s/\\$/\\$\\$/g
```

## Let's Encrypt `acme.json`
Traefik saves all necessary informaion regarding the certificates as JSON in the `acme.json`. This file needs specific rights:

```bash
cd letsencrypt
# the acme-sample.json is empty in the beginning and will be filled during the certificate handshake
mv acme-sample.json acme.json
chmod 600 acme.json
```

## docker-compose `.env`
In the `.env` file we store the Duck DNS `domain name` and the Duck DNS `token`:

```bash
mv .env-sample .env
```

Change the following values to your own `Duck DNS`values:

```bash
DOMAINNAME=your.duckdns.org
DUCKDNS_TOKEN=duckdns-token
```

## The `traefik.toml`
Sample Traefik configuration with `Docker`, `Let's Encrypt` and `Duck DNS`

```bash
cd config
mv traefik-sample.toml traefik.toml
```

Change the example values to your own needs.

## The `dynamic_config.yml`
With the sample configuration in the `dynamic_config-sample.yml` the security requirements are very high and reach an `A` rating at the [SSLLabs Test](https://www.ssllabs.com/ssltest)
(Only current Browser versions support this strict configuration)

```bash
cd config
mv dynamic_config-sample.yml dynamic_config.yml
```

Change the example values of routers and services accordingly to your own needs.

