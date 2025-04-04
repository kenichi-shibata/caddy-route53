
## Usage

This image is used to run Caddy with the Route53 DNS module for automatic TLS certificate management using AWS Route 53.

## Building the image

To build the image, run the following command:

docker image for caddy with route53 module by default

Here's the Dockerfile:

```dockerfile
FROM caddy:builder AS builder

RUN xcaddy build \\
    --with github.com/caddy-dns/route53

FROM caddy:latest

COPY --from=builder /usr/bin/caddy /usr/bin/caddy
```


To build this Dockerfile, navigate to the directory containing the Dockerfile and run:

```bash
docker build -t caddy-route53 .
```

This command builds the Docker image and tags it as `caddy-route53`.


### Building for amd64 on an M1 Macbook

To build an `amd64` image on an M1 Macbook, you can use Docker's buildx feature. First, make sure buildx is set up:

```bash
docker buildx create --name multi-arch-builder --driver docker-container --bootstrap
docker buildx use multi-arch-builder
docker buildx inspect --bootstrap
```

Then, build the image specifying the platform:

```bash
docker buildx build --platform linux/amd64 -t caddy-route53-amd64 .
```

This command builds the Docker image for the `linux/amd64` platform and tags it as `caddy-route53-amd64`.


## Pushing the image to Docker Hub

After building the image, you can tag and push it to Docker Hub.

First, tag the image with your Docker Hub username and a tag name:

```bash
docker tag caddy-route53 kenichishibata/caddy-route53:tagname
```

Replace `tagname` with the desired tag name (e.g., `latest`, `v1.0.0`).

Then, push the image to Docker Hub:

```bash
docker push kenichishibata/caddy-route53:tagname
```

Make sure you are logged in to Docker Hub before pushing. You can log in using the `docker login` command.