[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/new/template/oneuptime-1?utm_medium=integration&utm_source=button&utm_campaign=oneuptime)

# OneUptime on Railway

One-click Railway template for [OneUptime](https://github.com/OneUptime/oneuptime) **16.0.0**: open-source uptime monitoring, status pages, incidents, on-call, logs, metrics and traces.

## What it deploys

| Service | Built from | What it does |
|---|---|---|
| `ingress` | `ingress/` (`oneuptime/nginx:16.0.0`) | nginx gateway, the only public service. Routes the dashboard, API, status pages and OTLP ingest to the app |
| `app` | `app/` (`oneuptime/app:16.0.0`) | Dashboard, API, status pages, background workers and telemetry ingest. Applies the database migrations on boot |
| `probe` | `probe/` (`oneuptime/probe:16.0.0`) | Runs your monitors (HTTP, ports, SSL, synthetic browser checks) and reports to the app |
| `runner` | `runner/` (`oneuptime/runner:16.0.0`) | The global runner for workflow and runbook steps |
| `clickhouse` | `clickhouse/` (`clickhouse/clickhouse-server:26.7.38.18`) | Telemetry and monitor-history store, volume at `/var/lib/clickhouse` |
| `Postgres` | Railway PostgreSQL | Application data, volume |
| `Redis` | Railway Redis | Cache and job queues, volume |

Every image is pinned by version and digest in the folder's `Dockerfile`. Services talk over Railway's private network with reference variables.

## Variables

Nothing to fill in. The template generates `ONEUPTIME_SECRET`, `ENCRYPTION_SECRET`, `REGISTER_PROBE_KEY`, `GLOBAL_RUNNER_KEY`, the probe key and the ClickHouse password, and wires the database, Redis and ClickHouse settings with references. `HOST` is the ingress's Railway domain. Fixed settings (ports, `HTTP_PROTOCOL=https`, telemetry off) are in the Dockerfiles; override any of them with a service variable.

After the first deploy, open the ingress URL and sign up: the first account is the instance admin. Then open `/admin/setup` to set up email (SMTP or an API provider) and, if you want, SMS and calls. Open sign-up can be closed in the Admin Dashboard.

Not included: OneUptime's optional ClamAV scanner, the second probe, and the UDP receivers of the probe (SNMP traps, syslog, NetFlow), which Railway can't expose. ICMP ping monitors may not work on Railway.

## Updates

Deployers of this template get Railway's "update available" notice when this repo's `main` changes. Each version bump changes the pinned image in the folders' Dockerfiles, and `CHANGELOG.md` lists what changed, breaking changes first. Back up Postgres and ClickHouse before a major OneUptime upgrade.
