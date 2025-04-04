
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