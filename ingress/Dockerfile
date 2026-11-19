# OneUptime ingress: nginx gateway in front of the app (routes, status pages, OTLP ingest),
# plus its Node sidecar for custom-domain certificates. The only public service.
FROM oneuptime/nginx:16.0.0@sha256:98535afad97d7280a54ece4fca1053d10eba661384eba4c94bc229f3d20d5e91

# Railway's private DNS server is an IPv6 address. nginx's `resolver` needs it in brackets,
# and upstream's run.sh writes it bare, so wrap it right after run.sh reads resolv.conf.
RUN sed -i '/^NGINX_RESOLVER=\$(grep/a case "$NGINX_RESOLVER" in *:*) case "$NGINX_RESOLVER" in \\[*) ;; *) NGINX_RESOLVER="[$NGINX_RESOLVER]" ;; esac ;; esac' /usr/src/app/run.sh \
 && grep -q 'NGINX_RESOLVER="\[\$NGINX_RESOLVER\]"' /usr/src/app/run.sh

# nginx serves the public site on 7849 (the Railway domain's target port).
# PORT is the Node sidecar's status port (7851), which Railway's health check calls.
ENV NODE_ENV=production \
    ENVIRONMENT=production \
    PORT=7851 \
    APP_PORT=3002 \
    HOME_PORT=3002 \
    HTTP_PROTOCOL=https \
    BILLING_ENABLED=false \
    IS_ENTERPRISE_EDITION=false \
    LOG_LEVEL=ERROR \
    DISABLE_TELEMETRY=true \
    RUN_DATABASE_MIGRATIONS_ON_BOOT=false \
    DATABASE_SSL_REJECT_UNAUTHORIZED=false \
    VALKEY_DB=0 \
    VALKEY_IP_FAMILY=0 \
    NGINX_LISTEN_ADDRESS= \
    NGINX_LISTEN_OPTIONS= \
    NGINX_INGEST_ACCESS_LOG=off

# Start command: the image's own CMD (./run.sh starts nginx and the sidecar).
