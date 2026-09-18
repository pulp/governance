# GitHub organization policies

This policy defines the target state for organization-wide configuration.

- See [Github Audit Process](/docs/github/audit-state.md) for guides on how to check them.
- See [Github Reference](/docs/github/reference.md) for github configuration capabilities reference.

## General

- [stricter-repo-settings] A repository MAY have stricter settings
- [no-weaker-repo-settings] A repository MUST NOT have less strict settings
- [policy-change-review] Changes to these organization policies SHOULD be reviewed before they are applied.

## Branch and tag lifecycle

- [no-legacy-branch] The organization MUST NOT use legacy branch protection rules.
  Use rulesets instead.
- [no-force-push-delete] Organization rulesets MUST disallow force pushes and deletion of protected branches and tags.
- [release-bot-only] Creation and pushing of release branches and tags MUST be limited to the release bot
  or an explicitly approved equivalent.

## Pull request merge gates

- [required-pull-request] Protected branches MUST require pull requests.
- [required-approval] Protected branches MUST require at least one approving review before merging.
- [required-ci-checks] Repositories with CI workflows MUST have required checks and they MUST pass before merging

## Actions and CI

- [restricted-actions] The organization MUST restrict which GitHub Actions can run.
- [external-workflow-approval] Workflows originating from external contributors MUST require approval before they run with repository access.
- [readonly-github-token] The default `GITHUB_TOKEN` permissions MUST be read-only.
- [declared-workflow-permissions] A workflow MUST NOT request additional permissions if not in a special workflow.
