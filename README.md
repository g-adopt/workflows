G-ADOPT Reusable Workflows
==========================

This repository contains [reusable workflows] for Actions across the
G-ADOPT organisation. Runners are whitelisted to workflows here on the
`main` and `test` branches.

[reusable workflows]: https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows

Development
-----------

Pull Requests should be based on `main` as usual. The `test` branch is
a mutable staging ref, used to test proposed changes before
merging. Changes must be manually reviewed before triggering a
validation run.

To test a candidate, move the `test` ref to the desired commit, e.g.

```
$ git push --force-with-lease origin HEAD:refs/heads/test
```

Then manually dispatch the calling workflow on the `ci-test` branch of
the downstream repository. This branch references the reusable
workflows at `@test`, e.g.

```yaml
jobs:
  example:
    uses: g-adopt/workflows/.github/workflows/example.yml@test
```

No secrets are stored in this repository's Actions configuration:
calling workflows should explicitly pass any required secrets to the
reusable workflow.
