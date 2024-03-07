# Dip Postgres

Postgres configuration for [Dip infra services](https://github.com/bibendi/dip).

## Usage

1. Add a service to the application's `dip.yml`.

```yaml
infra:
  postgres:
    git: https://github.com/bibendi/dip-postgres.git
```

2. Add a network to the application's `docker-compose.yml`.

```yaml
networks:
  postgres-net:
    name: ${DIP_INFRA_NETWORK_POSTGRES}
    external: true
```

Where `DIP_INFRA_NETWORK_POSTGRES` is a special variable that is set by Dip.

3. Add a `POSTGRES_URL` environment variable and the `postgres-net` to a Docker Compose service.

```yaml
services:
  app:
    environment:
      DATABASE_URL: postgres://postgres:keepinsecret@postgres:5432
    networks:
      - default
      - postgres-net
```

4. Start infra services.

```sh
dip infra up
```

5. Start the app

```sh
dip up
```
