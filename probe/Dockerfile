# OneUptime probe: runs the monitor checks (HTTP, ports, SSL, synthetic browser checks)
# and reports them to the app over the private network.
FROM oneuptime/probe:16.0.0@sha256:da86019a895847cce2decddaa054c08ee1df6e8c6ae1386bfbc79d32dfce7481

# Railway exposes no UDP ports, so the probe's SNMP-trap, syslog and NetFlow receivers stay off.
ENV NODE_ENV=production \
    PORT=3874 \
    PROBE_NAME="Railway Probe" \
    PROBE_DESCRIPTION="Global probe bundled with the Railway template" \
    PROBE_MONITORING_WORKERS=5 \
    PROBE_MONITOR_FETCH_LIMIT=10 \
    PROBE_SYNTHETIC_MONITOR_SCRIPT_TIMEOUT_IN_MS=60000 \
    PROBE_CUSTOM_CODE_MONITOR_SCRIPT_TIMEOUT_IN_MS=60000 \
    PROBE_SNMP_TRAP_RECEIVER_ENABLED=false \
    PROBE_SYSLOG_RECEIVER_ENABLED=false \
    PROBE_NETFLOW_RECEIVER_ENABLED=false \
    LOG_LEVEL=ERROR \
    DISABLE_TELEMETRY=true

# Start command: the image's own ENTRYPOINT (tini) and CMD.
