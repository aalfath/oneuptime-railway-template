# OneUptime app: dashboard, API, status pages, workers and telemetry ingest in one process.
# Upstream image, pinned by version and digest. Bump both together (see CHANGELOG.md).
FROM oneuptime/app:16.0.0@sha256:7a319a7ee863913d40ef8c3cddef6ad3e4379861a65e3dd88afc82569b522ac9

# Fixed settings for Railway. Anything here can be overridden with a service variable.
# The app applies its PostgreSQL and ClickHouse migrations itself on boot.
ENV NODE_ENV=production \
    ENVIRONMENT=production \
    PORT=3002 \
    APP_PORT=3002 \
    HOME_PORT=3002 \
    HTTP_PROTOCOL=https \
    BILLING_ENABLED=false \
    IS_ENTERPRISE_EDITION=false \
    LOG_LEVEL=ERROR \
    DISABLE_TELEMETRY=true \
    DATABASE_SSL_REJECT_UNAUTHORIZED=false \
    CLICKHOUSE_PORT=8123 \
    CLICKHOUSE_USER=oneuptime \
    CLICKHOUSE_DATABASE=oneuptime \
    VALKEY_DB=0 \
    VALKEY_IP_FAMILY=0 \
    GLOBAL_RUNNER_REPLICAS=1 \
    TRUSTED_PROXY_HOPS=2

# Start command: the image's own CMD (sizes the Node heap from the container's memory limit).
