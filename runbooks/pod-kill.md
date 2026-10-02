# Runbook: Pod Kill / Unexpected Pod Termination

## Detection
Alert fires: `KubePodCrashLooping` or availability drop in Grafana.

## Immediate steps
1. `kubectl get pods -n default -l app=sample-service` — check restart count / status
2. `kubectl describe pod <pod>` — check events for OOMKilled vs evicted vs killed
3. `kubectl logs <pod> --previous` — check last logs before death
4. Check Dynatrace Davis AI problem feed for correlated anomalies

## Mitigation
- If replica count dropped below minReplicas, confirm HPA/ReplicaSet is recovering pods
- If recurring, check node health (`kubectl describe node`) for resource pressure

## Escalation
Page secondary on-call if not recovered within 15 minutes or SLO burn rate > 2x.
