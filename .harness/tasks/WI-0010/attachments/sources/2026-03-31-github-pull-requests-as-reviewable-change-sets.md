# Source Note

- Linked work items: WI-0010


- Date: 2026-03-31
- Source: GitHub pull requests as reviewable change sets
- URL: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests?platform=mac
- Type: official product documentation
- Accessed date: 2026-03-31
- Trust level: high
- Notes:
  - GitHub defines a pull request as a proposal to merge changes from one branch into another.
  - The docs describe pull requests as the place where collaborators review and discuss the proposed change set before integration.
  - GitHub also documents draft pull requests as the correct way to expose work-in-progress without formally requesting review yet.

## Optional Detail

- Topic: GitHub pull requests as reviewable change sets
- Publisher or owner: GitHub Docs
- Published date: none
- Claim area: reviewable diffs and work-in-progress boundaries
- Supports:
  - Review readiness should map to a bounded proposed diff, not only to a task status label.
  - When the worktree is still mixed, the system should prefer blocker or draft semantics over pretending the slice is ready for acceptance.
- Conflicts with:
  - Treating a `review` task as reviewable when the source boundary is no longer one coherent proposal.
