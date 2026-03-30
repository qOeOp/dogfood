# Status Snapshot

- Linked work items: WI-0002


- Date: 2026-03-29
- Label: research_ctl ingest-local tool failure 203250
- Flush boundary: research_ctl ingest-local exited with code 0 before durable evidence was produced
- Crash-safe through: task-local failure checkpoint was written and recovery now points to the failed invocation boundary
- New decisions: none
- Open risks: task-scoped research command failed: file not found: /tmp/definitely-missing-research-file.md 
- Follow-ups: './.agents/skills/harness/scripts/research_ctl.sh' --work-item 'WI-0002' 'ingest-local' '/tmp/definitely-missing-research-file.md'
- What changed in current state: research_ctl ingest-local failed during task-scoped evidence collection

## Failure Record

- Tool: research_ctl ingest-local
- Exit code: 0
- Command: './.agents/skills/harness/scripts/research_ctl.sh' --work-item 'WI-0002' 'ingest-local' '/tmp/definitely-missing-research-file.md'
- Summary: task-scoped research command failed: file not found: /tmp/definitely-missing-research-file.md 
- Failure output file: /var/folders/n3/7bzqqwbn019gzxk79l7h6pt40000gn/T/tmp.eVDAuQM2kY

### Captured output

```text
file not found: /tmp/definitely-missing-research-file.md
```
