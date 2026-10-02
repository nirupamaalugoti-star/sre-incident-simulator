# SRE Incident Response Simulator

**What this demonstrates:** SLOs/SLIs, error budgets, chaos engineering, structured incident response,
and postmortem writing — the SRE skills that job postings screen for above raw tool knowledge.

## Architecture
A small K8s app (2-3 services) with deliberately injected failure modes, observed through
Grafana + Dynatrace, with runbooks and postmortems written for each incident type.

## Failure scenarios (chaos-experiments/)
1. **Pod kill under load** — random pod termination via Chaos Mesh while load-testing with k6
2. **Network latency injection** — simulate a slow downstream dependency
3. **Resource exhaustion** — CPU/memory stress on a node to trigger evictions
4. **Dependency failure** — kill a database connection pool mid-traffic

## How to run
```bash
kubectl apply -f k8s/            # deploy the sample services
kubectl apply -f chaos-experiments/pod-kill.yaml
# watch Grafana dashboard while it runs, then:
```
Fill in `runbooks/<scenario>.md` DURING the incident (as if paged), then write
`postmortems/<scenario>.md` after, following the template below.

## Postmortem template (use for every scenario)
- **Impact**: what broke, for how long, what SLO was breached
- **Timeline**: detection -> diagnosis -> mitigation -> resolution
- **Root cause**
- **What went well / what didn't**
- **Action items** with owners

## Resume bullet template
"Simulated production incident scenarios (pod failures, latency injection, resource exhaustion) using
Chaos Mesh; defined SLOs/error budgets and authored runbooks + postmortems following SRE incident
response best practices."
