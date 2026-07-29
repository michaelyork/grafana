# Grafana

This repository is the deployment source for the general-purpose Grafana
instance running on Coolify at `https://grafana.york.network`.

It is intentionally separate from TeslaMate's dedicated Grafana instance at
`https://grafana.teslamate.york.network`.

## Services

- Grafana `13.1.1` on container port `3000`
- PostgreSQL `17.4`
- Grafana Clock panel `3.2.2`, retained for the UniFi dashboard

The PostgreSQL service has no published host port. Grafana is reachable only
through Coolify's reverse proxy.

## Coolify configuration

Deploy the root `docker-compose.yml` using Coolify's Docker Compose build pack.
Assign this service domain:

- `grafana`: `https://grafana.york.network:3000`

Set the required `GRAFANA_SECRET_KEY` in Coolify. Coolify generates the database
and Grafana administrator passwords from the `SERVICE_PASSWORD_*` variables in
the Compose file.

The `:3000` suffix in Coolify's domain field is the destination container port;
clients still connect to normal HTTPS port `443`.

## Content ownership

This instance owns general infrastructure dashboards, including UniFi,
Prometheus, rack, utility, and uptime monitoring. TeslaMate dashboards and its
PostgreSQL datasource belong only in the dedicated TeslaMate Grafana instance.
