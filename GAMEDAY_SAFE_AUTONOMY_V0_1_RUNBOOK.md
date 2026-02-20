## Objective
Validate controlled recovery behavior:
1. Primary node failure detection
2. Failover to approved secondary
3. Restore failed node from verified snapshot
4. Rejoin after soak
5. Publish incident report with RTO/RPO

---

## Preconditions
- [ ] #1–#4 merged
- [ ] Test suite passing
- [ ] Kill switch + pause mode available
- [ ] Latest snapshot exists and integrity check passes
- [ ] Operator on-call assigned

---

## Roles
- Incident Commander (IC):
- Operator:
- Observer/Scribe:

---

## Environment
- Primary node:
- Secondary node (allowlisted):
- Snapshot ID/version:
- Policy version/hash:
- Budget limits:
- Alert channel:

---

## Timeline Steps

### T-15 min: Baseline
- [ ] Capture status (health/mode/freeze state)
- [ ] Capture policy hash
- [ ] Verify audit signatures
- [ ] Start timeline notes

### T0: Inject Primary Failure
- [ ] Simulate controlled primary failure
- [ ] Record failure inject timestamp
- [ ] Record detection timestamp

### Failover
- [ ] Confirm failover to allowlisted secondary
- [ ] Record failover complete timestamp
- [ ] Confirm service healthy on secondary

### Restore
- [ ] Verify snapshot integrity
- [ ] Restore failed primary from known-good snapshot
- [ ] Record restore start/end timestamps

### Rejoin + Soak
- [ ] Rejoin restored primary
- [ ] Start soak (15–30 min)
- [ ] Monitor error rate/latency/drift
- [ ] Record soak end timestamp

---

## Abort Criteria (STOP_NOW)
Abort immediately if:
- Unapproved migration target
- Budget guardrail bypass
- Audit signature verification failure
- Control-plane instability

On abort:
1. Trigger STOP_NOW
2. Preserve logs/evidence
3. Move to postmortem

---

## Success Criteria
- [ ] Detection within target
- [ ] Failover to allowlisted target only
- [ ] Restore from verified snapshot only
- [ ] Stable rejoin through soak
- [ ] Audit trail complete and verifiable
- [ ] Budget guardrails enforced

---

## Metrics
- RTO = failure inject → healthy secondary
- RPO = data gap vs replication/snapshot
- Alert latency
- Restore duration
- Soak stability metrics

---

## Incident Report Template

### Summary
- Date/time:
- Environment:
- Outcome: PASS / PARTIAL / FAIL

### Timeline
- T0 failure injected:
- Detection:
- Failover complete:
- Restore started:
- Restore completed:
- Rejoin completed:
- Soak completed:

### Results
- RTO:
- RPO:
- Audit verification:
- Budget guardrails:
- Policy compliance:

### What Worked
- 

### Risks / Gaps
- 

### Follow-ups
- [ ] Action — Owner — Due date
- [ ] Action — Owner — Due date
