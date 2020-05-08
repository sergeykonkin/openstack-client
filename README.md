# OpenStack Docker Client

OpenStack Client in Docker.

Current client version is `5.2.0`.

## Supported tags

* `5.2.0`, `latest`

## Usage

You can mount `your-openrc.sh` (which can be downloaded from OpenStack's web interface) to container's `/data/openrc.sh` which will be executed before starting OpenStack client:

```bash
docker run -it --rm -v "$(pwd)/your-openrc.sh:/data/openrc.sh:ro" sergeykonkin/openstack-client
# or via env variables using `.env` file:
docker run -it --rm --env-file ./openrc.env sergeykonkin/openstack-client
```

This will start OpenStack client in interactive mode.

Alternatively, you can pass arguments to run a single command:
```bash
docker run -it --rm -v "$(pwd)/your-openrc.sh:/data/openrc.sh:ro" sergeykonkin/openstack-client server list
```

## Usage as base image

Use this image to build your own client with the predefined environment:

```Dockerfile
FROM sergeykonkin/openstack-client

ENV OS_AUTH_URL="https://your-openstack.example.com"
ENV OS_PROJECT_ID="<your-project-id>"
ENV OS_PROJECT_NAME="<your-project-name>"
ENV OS_PROJECT_DOMAIN_ID="<your-domain-id>"
ENV OS_USER_DOMAIN_NAME="<your-domain-name>"
ENV OS_USERNAME="<your-username>"
ENV OS_INTERFACE="public"
ENV OS_IDENTITY_API_VERSION=3

ENTRYPOINT [ "openstack" ]
```
