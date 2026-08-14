# Deployment Blueprint

This document describes the target operational topology. The CodeSentinel application image and source are not public yet; only PostgreSQL and Redis can currently be started from the example Compose file.

## Environments

| Environment | Intended use | Persistence | Repair sandbox |
|---|---|---|---|
| Development | Local configuration and integration | Local Docker volumes | Optional Docker sandbox |
| CI | Pull-request gating | Ephemeral | Required, network disabled |
| Staging | End-to-end validation | Managed PostgreSQL/Redis | Dedicated worker pool |
| Production | Controlled organization deployment | Managed and backed up | Isolated nodes or containers |

## Configuration preparation

```bash
cp .env.example .env
docker compose -f deploy/docker-compose.example.yml config
```

Set `POSTGRES_PASSWORD`, `MODEL_API_KEY`, repository credentials, and telemetry endpoints through a secret manager or deployment environment. Do not store them in Git.

## Infrastructure-only startup

```bash
docker compose -f deploy/docker-compose.example.yml up -d postgres redis
docker compose -f deploy/docker-compose.example.yml ps
```

## Application startup

The following command is reserved for the implementation release:

```bash
docker compose -f deploy/docker-compose.example.yml --profile app up -d
```

The `unreleased` default image tag is intentional and prevents this blueprint from being mistaken for a currently runnable distribution.

## Worker topology

- One orchestrator accepts review jobs and coordinates barriers.
- Six review-worker replicas consume specialist tasks in parallel.
- One repair-worker replica handles eligible findings serially.
- PostgreSQL stores jobs, findings, verification records, and audit events.
- Redis provides queues, leases, locks, and transient coordination.

## Production controls

- Replace local volumes with managed storage and backups.
- Run repair workers on isolated nodes without host credentials.
- Do not mount the host Docker socket in production; use a dedicated sandbox service.
- Restrict egress from review and repair workloads.
- Enforce per-job CPU, memory, disk, token, and time limits.
- Redact source content from traces and application logs.
- Configure readiness probes and disruption budgets.
- Rotate repository and model-provider credentials.

## Validation checklist

```text
[ ] Compose configuration resolves without warnings
[ ] PostgreSQL and Redis health checks pass
[ ] Secrets are injected outside version control
[ ] Six review workers are registered
[ ] One repair worker is registered
[ ] Repair network access is disabled by default
[ ] Artifact and workspace retention is configured
[ ] Metrics, traces, and redaction policies are active
[ ] Backup and recovery procedures are tested
```

