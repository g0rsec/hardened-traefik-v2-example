# Hardened Traefik V2 example
## Features
- Use of a security-enhanced **proxy for the Docker Socket**.
- Use of [gVisor](https://github.com/google/gvisor) application kernel.
- Use of **non-root user** (1000:1000).
- HTTP scheme force redirect to HTTPS.
- Use of security headers to obtain **SSL A+ rank** on [Qualys SSL Labs](https://www.ssllabs.com/ssltest).

## Requirements
- [Docker](https://docs.docker.com/get-docker/)
- [Docker-compose](https://docs.docker.com/compose/install/)
- [gVisor](https://gvisor.dev/docs/user_guide/install/)

## Changes needed

In *./config/traefik.dynamic.toml* change dashboard auth middleware credentials and replace *domain.tld* to match personal domain configuration.
```bash
htpasswd -nbB username 'password'
```
In *./config/traefik.toml* change email address used for ACME registration.  
In *./docker-compose.yml* replace *domain.tld* to match personal domain configuration.  

## Deployment
```bash
chmod 600 logs/access.log; chmod 600 config/acme.json; chmod 400 config/traefik.toml; chmod 400 config/traefik.dynamic.toml
chown -R 1000:1000 logs config
docker-compose up -d
```
