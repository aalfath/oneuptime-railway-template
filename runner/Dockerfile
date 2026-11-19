# OneUptime global runner: runs workflow and runbook steps (JavaScript, Bash, HTTP) for every project.
FROM oneuptime/runner:16.0.0@sha256:efcab9c06d8e3b88b10bf5f32064e26f83d9374fcc33600da8335b4df848fcd6

# The fixed id of the bundled global runner (Common/Types/Runner/BundledGlobalRunner.ts upstream).
ENV NODE_ENV=production \
    PORT=3877 \
    ONEUPTIME_RUNNER_ID=00000000-0000-0000-0000-000000000002 \
    ONEUPTIME_RUNNER_CONCURRENCY=4 \
    ONEUPTIME_RUNNER_ENABLE_AI_COMMANDS=false \
    LOG_LEVEL=ERROR \
    DISABLE_TELEMETRY=true

# Start command: the image's own ENTRYPOINT (tini) and CMD.
