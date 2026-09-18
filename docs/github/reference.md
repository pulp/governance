# GitHub configuration reference

This is a gentle reference to GitHub configurations.

The goal is to get a feeling of the options and general structure.
For authoritative information, see the appropriate section of the documentation.

## Introduction

GitHub configuration is spread across organization and repository settings, and the
same concept is sometimes available in both places. The easiest way to understand it
is to group settings by the job they perform:

- **Governance and merge protection** decide which changes may enter a branch or tag.
  Rulesets are the modern, composable way to express these controls.
- **Actions and CI** decide which automation is allowed to run and what it can do.
  Action policies are the boundary; action configuration supplies permissions,
  runners, secrets, and variables.
- **Code security** enables detection and prevention features such as Dependabot,
  secret scanning, push protection, and CodeQL.
- **Deployments** protect delivery targets with environments, approvals, wait timers,
  and branch restrictions.
- **People and repository access** determine who can discover, administer, review,
  and write to repositories.
- **Repository metadata and collaboration** cover features such as CODEOWNERS,
  custom properties, moderation, and repository-level defaults.

Depending on the feature, organization settings can be repository defaults,
enforcement boundaries, or independent from repository settings.

The paths below use a consistent shorthand for the GitHub web UI:
`Organization/Settings/...` means the organization settings, and `Repository/Settings/...` means a
repository's settings.

## Governance and merge protection

### Rulesets

Rulesets enforce controls across branches, tags, or pushes. They can require pull
request reviews and status checks, prevent deletion or force pushes, restrict who
can bypass a rule, and target several repositories from an organization. They are
the successor to legacy branch protection rules.

- Organization: `Organization/Settings/Repository/Rulesets`
- Repository: `Repository/Settings/Code and automation/Rules/Rulesets`
- Reference: [About rulesets](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets)
- Available controls: [Available rules for rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets)

### Repository policies

Repository policies are organization-level controls for governing how people use
repositories. They are currently in public preview and subject to change. Where
available, evaluate them alongside rulesets rather than assuming that a repository
setting is sufficient.

- Organization: `Organization/Settings/Policies/Repository`
- Repository: `Repository/Settings/Policies/Repository`
- Reference: [Governing how people use repositories in your organization](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/governing-how-people-use-repositories-in-your-organization)

## Actions and CI

### Action policies

Action policies define what workflows and actions are allowed to execute. They may
restrict actions to the organization, approved actions, or pinned references, and
can set boundaries that repositories cannot exceed. Approval of workflows from fork
or external contributors is also an important part of this group.

- Organization: `Organization/Settings/Actions/General`
- Repository: `Repository/Settings/Actions/General`
- Policy rules (where enabled): `Organization/Settings/Actions/Policies` and
  `Repository/Settings/Actions/Policies`
- Reference: [Disabling or limiting GitHub Actions](https://docs.github.com/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization)

### Action configuration

Action configuration controls runtime behavior: `GITHUB_TOKEN` default permissions,
workflow permissions, runner groups, and secrets and variables. Organization values
may be defaults or ceilings; repository values should be checked separately.
Action policies govern what may run and when forked workflows may run; action
configuration governs the capabilities and resources available once they run.

- Organization: `Organization/Settings/Actions/General`
- Organization secrets and variables: `Organization/Settings/Actions/Secrets and variables`
- Repository: `Repository/Settings/Actions/General`
- Repository secrets and variables: `Repository/Settings/Secrets and variables/Actions`
- Reference: [Managing GitHub Actions settings for a repository](https://docs.github.com/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)

## Code security

Code security configurations manage Secret Scanning, push protection, Dependabot,
and code scanning (including CodeQL). GitHub can apply these centrally to a set of
repositories or configure them one repository at a time.
Feature availability depends on the GitHub plan and repository eligibility; an audit
should distinguish enabled features from features effectively applied to a repository.

- Organization: `Organization/Settings/Code security and analysis/Configurations`
- Repository: `Repository/Settings/Security/Code security and analysis`
- Reference: [About GitHub code security](https://docs.github.com/code-security/securing-your-organization/introduction-to-github-code-security/about-github-code-security)

## Deployments

Environments are repository-scoped deployment targets. They can require reviewers,
add wait timers, restrict deployment branches, and provide environment-scoped
secrets and variables. Their effective protection also depends on whether
administrators can bypass protection rules and whether custom deployment protection
rules are enabled.

- Repository: `Repository/Settings/Environments`
- Reference: [Using environments for deployment](https://docs.github.com/actions/deployment/targeting-different-environments/using-environments-for-deployment)

## People and repository access

Organization member privileges establish the baseline access level and available
roles. Repository collaborators and teams then provide repository-specific access.
Review these together: a repository can look permissive because of either its
organization base permission or a direct/team grant.
Organization owners, GitHub Apps, deploy keys, and service accounts are separate
privileged access paths and should be reviewed independently.

- Organization: `Organization/Settings/Member privileges`
- Repository: `Repository/Settings/Access/Collaborators and teams`
- Reference: [Repository roles for an organization](https://docs.github.com/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization)

## Repository metadata and collaboration

Custom properties are useful for grouping repositories and applying targeted rules,
for example requiring a plugin-specific CI check without applying it to docs or CLI
repositories. Their definitions are organization-managed, while repositories hold
the individual values used for targeting. CODEOWNERS can assign ownership for
sensitive paths. Moderation and review settings can limit who may review or
interact with code.

- Custom-property definitions: `Organization/Settings/Repositories/Custom properties`
- Custom-property values: each repository
- CODEOWNERS: `.github/CODEOWNERS` (or `CODEOWNERS` at the repository root)
- Code review limits: `Organization/Settings/Access/Moderation/Code review limits` and
  `Repository/Settings/Access/Moderation/Code review limits`
- Reference: [Custom properties](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization)
- Reference: [About CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
