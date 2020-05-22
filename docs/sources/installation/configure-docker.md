+++
title = "Configure ThingSPIN Docker image"
description = "Guide for configuring the ThingSPIN Docker image"
keywords = ["grafana", "configuration", "documentation", "docker"]
type = "docs"
[menu.docs]
name = "Configure ThingSPIN Docker image"
identifier = "docker"
parent = "administration"
weight = 650
+++

# Configure a ThingSPIN Docker image

If you are running ThingSPIN in a Docker image, then you configure ThingSPIN using [environment variables]({{< relref "configuration.md#configure-with-environment-variables" >}}) rather than directly editing the configuration file. If you want to save your data, then you also need to designate persistent storage or bind mounts for the ThingSPIN container.

## Save your ThingSPIN data

If you do not designate a location for information storage, then all your ThingSPIN data disappears as soon as you stop your image. To save your data, you need to set up persistent storage or bind mounts for your container.

### Run ThingSPIN container with persistent storage (recommended)

```bash
# create a persistent volume for your data in /var/lib/grafana (database and plugins)
docker volume create grafana-storage

# start grafana
docker run -d -p 3000:3000 --name=grafana -v grafana-storage:/var/lib/grafana grafana/grafana
```

### Run ThingSPIN container using bind mounts

You may want to run ThingSPIN in Docker but use folders on your host for the database or configuration. When doing so, it becomes important to start the container with a user that is able to access and write to the folder you map into the container.

```bash
mkdir data # creates a folder for your data
ID=$(id -u) # saves your user id in the ID variable

# starts grafana with your user id and using the data folder
docker run -d --user $ID --volume "$PWD/data:/var/lib/grafana" -p 3000:3000 grafana/grafana:5.1.0
```

## Default paths

The following settings are hard-coded when launching the ThingSPIN Docker container and can only be overridden using environment variables, not in `conf/grafana.ini`.

Setting               | Default value
----------------------|---------------------------
GF_PATHS_CONFIG       | /etc/grafana/grafana.ini
GF_PATHS_DATA         | /var/lib/grafana
GF_PATHS_HOME         | /usr/share/grafana
GF_PATHS_LOGS         | /var/log/grafana
GF_PATHS_PLUGINS      | /var/lib/grafana/plugins
GF_PATHS_PROVISIONING | /etc/grafana/provisioning

## Configure ThingSPIN with Docker Secrets

> Only available in ThingSPIN v5.2 and later.

It's possible to supply ThingSPIN with configuration through files. This works well with [Docker Secrets](https://docs.docker.com/engine/swarm/secrets/) as the secrets by default gets mapped into `/run/secrets/<name of secret>` of the container.

You can do this with any of the configuration options in conf/grafana.ini by setting `GF_<SectionName>_<KeyName>__FILE` to the path of the file holding the secret.

For example, you could set the admin password this way:

- Admin password secret: `/run/secrets/admin_password`
- Environment variable: `GF_SECURITY_ADMIN_PASSWORD__FILE=/run/secrets/admin_password`

## Configure AWS credentials for CloudWatch Support

```bash
docker run -d \
-p 3000:3000 \
--name=grafana \
-e "GF_AWS_PROFILES=default" \
-e "GF_AWS_default_ACCESS_KEY_ID=YOUR_ACCESS_KEY" \
-e "GF_AWS_default_SECRET_ACCESS_KEY=YOUR_SECRET_KEY" \
-e "GF_AWS_default_REGION=us-east-1" \
grafana/grafana
```

You may also specify multiple profiles to `GF_AWS_PROFILES` (e.g.
`GF_AWS_PROFILES=default another`).

Supported variables:

- `GF_AWS_${profile}_ACCESS_KEY_ID`: AWS access key ID (required).
- `GF_AWS_${profile}_SECRET_ACCESS_KEY`: AWS secret access  key (required).
- `GF_AWS_${profile}_REGION`: AWS region (optional).
