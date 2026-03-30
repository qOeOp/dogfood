# Status Snapshot

- Linked work items: WI-0008

- Date: 2026-03-29
- Label: compounding target semantics acceptance closeout
- Flush boundary: work-object-relative compounding semantics landed in canonical instructions, source/runtime validation passed, acceptance artifacts are linked, and terminal transition to `done` completed before this checkpoint
- Crash-safe through: `WI-0008` is `done`, the framework now compounds the current work object by default, and reopening can start from the acceptance brief if stronger routing is later needed
- New decisions: make compounding target selection follow the current work object; in this dogfood round harness is the target only because harness is the active work object being iterated
- Open risks: ambiguous feedback can still require judgment when the active work object is unclear, so a future typed routing/control surface may still be worth exploring on recurrence
- Follow-ups: resume `WI-0004`; only open a stronger typed-routing task if later runs prove the wording+validator layer insufficient
- What changed in current state: the framework no longer oscillates between "always compound harness" and "swallow all project feedback"; it now has a validator-backed default that compounds the thing currently being improved
