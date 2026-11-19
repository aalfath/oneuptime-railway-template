# ClickHouse for OneUptime's logs, metrics, traces and monitor history.
# OneUptime 16.0.0 pins ClickHouse 26.7 (docker-compose.base.yml upstream).
FROM clickhouse/clickhouse-server:26.7.38.18@sha256:503d89887bcc767ad3f00864259f57a6ee842c3ebedc53a62889f5ed6cdc1360

# Upstream's drop-ins, copied unchanged from OneUptime 16.0.0 (Clickhouse/ in OneUptime/oneuptime):
# a one-node "oneuptime" cluster with embedded Keeper (the schema is ReplicatedMergeTree + Distributed),
# batched Distributed inserts, 6-hour TTL on ClickHouse's own system logs, and warning-level logging.
COPY config.d/ /etc/clickhouse-server/config.d/
COPY users.d/ /etc/clickhouse-server/users.d/

# The image's entrypoint creates this user and database on first start.
# CLICKHOUSE_PASSWORD comes from the template (a generated secret).
ENV CLICKHOUSE_USER=oneuptime \
    CLICKHOUSE_DB=oneuptime \
    CLICKHOUSE_DEFAULT_ACCESS_MANAGEMENT=1 \
    PORT=8123

# Data, Keeper logs and snapshots live under /var/lib/clickhouse (the Railway volume).
# Start command: the image's own ENTRYPOINT (/entrypoint.sh).
