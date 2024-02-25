

# Reserved Directories

These are standardized and reserved directories on the root server that are used to provide configuration and state between containers.

| Directory | Purpose | Consumers |
| ---       | ---     | ---       |
| `/var/opt/traefik` | Used to store global configuration for traefik | [traefik](./compose/traefik/) |
| `/var/opt/ssl` | Stores SSL certificates for web applications | [traefik](./compose/traefik/) |
