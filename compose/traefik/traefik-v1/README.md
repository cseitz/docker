
Based off https://github.com/ChristianLempa/boilerplates/tree/main/docker-compose/traefik

https://youtu.be/wLrmmh1eI94?si=0YM5vprwkr8D2qjb

# Deploying

1. Copy the `config` directory to `/var/opt/traefik`
2. Update `traefik.yml` as needed
3. Deploy `docker-compose.yml` via Portainer

## TLS

```bash
mkdir -p /var/opt/traefik/config/certs
```

https://youtu.be/NzSdNoR-JPo?si=z4qG5TfrVz6KNxxE

See video linked above and modify the `traefik.yml` to connect to Cloudflare for TLS.

1. Fill out `Configure your CertificateResolver here` section in `traefik.yml`
2. Uncomment `Disable TLS Cert verification check` section in `traefik.yml`

# Containers

You need to set the docker containers' network to `frontend` or `backend`. Be sure to include `external` flag.

```yml
networks:
  frontend:
    external: true

services:
  myapp:
    labels:
      - traefik.enable=true
    networks:
      - frontend
```

## Entrypoint

- `traefik.http.routers.[router-name].entrypoints` = `web`
- `traefik.http.routers.[router-name].rule` = `Host(\`subdomain.domain.com\`)`

## TLS


- `traefik.http.routers.[router-name].entrypoints` = `web, websecure`
- `traefik.http.routers.[router-name].tls` = `true`
- `traefik.http.routers.[router-name].tls.certresolver` = `staging` or `production`. 
  - Start by using `staging`, this will incur no acme rate limiting but certs will not be trusted.
  - Once you are sure it works, change `certresolver` to `production`.

### Optional: Automatically redirect to HTTPS

- `traefik.http.middlewares.[router-name].redirectscheme.permanent` = `true`
- `traefik.http.middlewares.[router-name].redirectscheme.scheme=https` = `redirect-to-https`



