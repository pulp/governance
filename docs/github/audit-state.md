# GitHub configuration audit state

This is a life audit document for the Pulp organization and repositories.

Until we automate it this can't be 100% reliable.

Pick a policy, check it's status and update the records.

## Individual Policy State Format

Proposed state representation for a policy.

### Enforceable

```
### [policy-id]

- Criteria for this policy to pass and hints in how to check
  - Scope: Organization|supported-repositories
  - Enforceable-orgwise: Unknown|Yes|No
  - Location: `repository-rulesets-org`
  - Status: Unknown|Failed|Pass
  - Notes:
  - Review-date: MM-DD-YY
```

Properties:

- Scope: the audit scope. Possible values: `Organization`, `Supported-repositories`. Default: `Organization`.
- Enforceable-orgwise: whether the setting that enabled this can be set only at the organization level. Default: Unknown.
- Location: the location of that enabling setting in the UI. See the location mapping down in the document.
            None means it's not directly configurable.
- Status: the audit result. Possible values: Unknown, Failing, Passing.
- Notes: free-form audit notes.
- Review-date: when the last review was performed for this item. Default: `MM-DD-YY`.

### Non-Enforceable

Doesn't have state properties.

```
### [policy-id]

General non-enforceable criteria or notes about this policy.
```

## Auditing

### General

#### [stricter-repo-settings]

A repository may have stricter settings.

#### [no-weaker-repo-settings]

Policies enforced by ruleset settings which are defined org-wise guarantees repository-level settings cannot be weaker than organization settings.
Some policies can't be enforced with rulesets, and this cascading behavior is not guaranteed.
Look at all settings which don't have org-cascading behavior and check it's true!

#### [policy-change-review]

Changes to these organization policies should be reviewed before they are applied.

### Branch and tag lifecycle

#### [no-legacy-branch]

- No legacy branch protection rule is still being used.
  - Scope: supported-repositories
  - Enforceable-orgwise: False
  - Location: `branches-legacy-repo`
  - Status: Failed
  - Notes: This is not enforceable, but there is a button for converting legacy to rulesets.
  - Review-date: 18-09-26

#### [no-force-push-delete]

- Force pushes and deletion are blocked for protected branches (release branches and main) and tags.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `repository-rulesets-org`
  - Status: Failed
  - Notes: Repositories looks like they have it set. Still, enforce at org-level.
  - Review-date: 18-09-26

#### [release-bot-only]

- Creation and pushing of release branches and tags are limited to the release bot or explicitly approved actors.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `repository-rulesets-org`
  - Status: Failed
  - Notes: Apparently most repositories don't protect tags. Enforce org-level
  - Review-date: 18-09-26

### Pull request merge gates

#### [required-pull-request]

- Pull requests are required for protected branches.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `repository-rulesets-org`
  - Status: Failed
  - Notes: Most repositories have this, but should be enforced org-level.
  - Review-date: 18-09-26

#### [required-approval]

- At least one approving review is required.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `repository-rulesets-org`
  - Status: Failed
  - Notes: Most repositories have this, but should be enforced org-level.
  - Review-date: 18-09-26

#### [required-ci-checks]

- Required CI status checks are present and required.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `repository-rulesets-org`
  - Status: Failed
  - Notes: Most repositories have this, but should be enforced org-level.
  - Review-date: 18-09-26

### Actions and CI

#### [restricted-actions]

- Allow organization-owned and selected actions and reusable workflows.
  Allow actions created by GitHub.
  Allow actions by Marketplace verified creators.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `actions-general-org`
  - Status: Pass
  - Notes: Even though it's not a rulest, the "keep stricter" rule is respected
  - Review-date: 18-09-26

#### [external-workflow-approval]

- Workflow approval is required for forks and other external contributors.
  - Scope: Organization
  - Enforceable-orgwise: No
  - Location: `actions-general-org`, `actions-general-repo`
  - Status: Failed
  - Notes:
      There are 3 options:

      1. Require approval for first-time contributors who are new to GitHub
      2. Require approval for first-time contributors
      3. Require approval for all external contributors

      Organization level is 2 but individual repos can be in 1 (e.g pulp_container).
      It should be 3.
  - Review-date: 18-09-26

#### [readonly-github-token]

- The default `GITHUB_TOKEN` permission is read-only.
  - Scope: Organization
  - Enforceable-orgwise: Yes
  - Location: `actions-general-org`, `actions-general-repo`
  - Status: Failed
  - Notes:
      The org default is read and write. Need to access the impact of globally restricting it
      and picture what's the best pratice here.
  - Review-date: 18-09-26

#### [declared-workflow-permissions]

- TODO: declare what workflows can require additional permissions and how.
  - Scope: Organization
  - Enforceable-orgwise: Unknown
  - Location: `actions-general-org`, `actions-general-repo`
  - Status: Unknown
  - Notes: This needs refinement. Or dropping.
  - Review-date: 18-09-26

## Policies declined

There are topics which were discussed and rejected.
Must provide the rejection reason.

None yet.

## Policies pending evaluation

There are topics which needs more research and discussion:

- whether actions must be pinned to commit SHAs
- whether we should use immutable releases
- whether we use commit signing
- whether merge methods and linear history should be standardized
- should we enforce policy for groups of repositories? this is possible through custom_properties
  - example, create groups for plugins (core vs community?), internal, experimental
- whether to allow GitHub Actions to create and approve pull requests
  - <https://docs.github.com/en/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization#preventing-github-actions-from-creating-or-approving-pull-requests>

## Location registry

The IDs refer to specific places in the GitHub UI.

- `repository-rulesets-org`: `Organization/Settings/Repository/Rulesets`
- `rulesets-repo`:           `Repository/Settings/Code and automation/Rules/Rulesets`
- `branches-legacy-repo`:    `Repository/Settings/Branches`
- `repository-policies-org`: `Organization/Settings/Policies/Repository`
- `actions-general-org`:     `Organization/Settings/Actions/General`
- `actions-policies-org`:    `Organization/Settings/Actions/Policies`
- `actions-general-repo`:    `Repository/Settings/Actions/General`
- `actions-policies-repo`:   `Repository/Settings/Actions/Policies`
- `actions-secrets-org`:     `Organization/Settings/Actions/Secrets and variables`
- `actions-secrets-repo`:    `Repository/Settings/Secrets and variables/Actions`
- `code-security-config-org`:`Organization/Settings/Code security and analysis/Configurations`
- `code-security-repo`:      `Repository/Settings/Security/Code security and analysis`
- `member-privileges-org`:   `Organization/Settings/Member privileges`
- `collaborators-repo`:      `Repository/Settings/Access/Collaborators and teams`
- `code-review-limits-org`:  `Organization/Settings/Access/Moderation/Code review limits`
- `code-review-limits-repo`: `Repository/Settings/Access/Moderation/Code review limits`
- `environments-repo`:       `Repository/Settings/Environments`
