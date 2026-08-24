# Pulp security policy

## Commitment

Red Hat takes security seriously.
Red Hat is committed to maintaining the highest level of security and trust for all users.
Red Hat appreciates the Pulp community and security researchers' efforts in helping identify and address vulnerabilities responsibly.

## Scope

This policy applies to all Pulp projects that Red Hat hosts.

### GitHub

Code contained in the [pulp](https://github.com/pulp) GitHub organization.

### Release artifacts

- Any Pulp releases from the above GitHub repos
- [Pulp PyPI releases](https://pypi.org/org/pulpproject/)

### Infrastructure

- `pulpproject.org`
- `*.pulpproject.org`
- `discourse.pulpproject.org`

## Maintained versions

Generally, only the latest release of an upstream project receives updates, including security patches.
Earlier versions may receive critical fixes on a best-effort basis, but back-porting to unsupported versions is not guaranteed.
End-of-Life versions receive no backports unless extraordinary circumstances warrant an exception approved by the Security Team.

Some projects may backport security fixes into multiple supported versions depending on severity.
See the development and stable version maintenance workflow documentation for details.

## Reporting a vulnerability

### How to report

All reports MUST be submitted by email to: <pulp-security@redhat.com>

Security vulnerabilities MUST NOT be reported through any public or insecure method, including but not limited to:

- Public GitHub issues
- Pull requests
- Pulp Discourse
- Pulp Matrix
- Public forums or social media

### What to include

When submitting a report, provide the following details:

- **Title** (required): Clear, descriptive summary
- **Reporter details** (optional): Your name/handle and affiliation
- **Impacted project** (required): Ideally link to the GitHub project
- **Vulnerability description** (required): Technical details of the issue
- **Affected versions** (required): Known affected version(s), and ideally all affected versions
- **Reproduction steps** (required): Minimal example to reproduce the issue
- **Impact assessment** (required): Potential exploit scenarios and severity
- **Suggested fix** (optional): Proposed remediation, if any
- **Disclosure status** (required): Whether and where this has been shared elsewhere

### What to report

Report if you have:

- Discovered a potential security vulnerability
- Found an issue but are uncertain about its security impact
- Identified vulnerabilities in dependencies not yet addressed

### What NOT to report

The following do not qualify as security vulnerabilities:

- Automated scanner output without analysis or reproduction steps
- General support or usage questions (use [Pulp Discourse](https://discourse.pulpproject.org))
- Requests for help updating to newer versions
- Bugs without security implications

Bugs that have no security impact should be filed through the public issues tracker of the respective GitHub project.

## Response process

The Pulp Security Team follows this process:

1. **Acknowledgment:** Confirms receipt of the report within one business day
1. **Triage:** Assesses validity and severity
1. **Investigation:** Reproduces and analyzes the issue
1. **Fix development:** Develops and tests a patch
1. **Coordinated disclosure:** Coordinates release timing with the reporter
1. **Public disclosure:** Publishes advisory and credits

## Severity classification

The Pulp project follows the [Red Hat severity ratings](https://access.redhat.com/security/updates/classification).

## Disclosure policy

- The Pulp project follows coordinated disclosure practices
- Fixes are typically included in the next planned release
- Critical vulnerabilities may warrant out-of-band releases
- Public disclosure occurs through GitHub Security Advisories
- Reporters are credited unless they prefer anonymity

For detailed information on disclosure types, embargo periods, and researcher coordination, see the [vulnerability management policy](vulnerability-management-policy.md).

## Security advisories

Security advisories are published through:

- [Pulp Discourse](https://discourse.pulpproject.org)
- CVE databases (NVD, OSV)

## The `SECURITY.md` file

`SECURITY.md` is the standard location where users, developers, and security researchers can find information on how to report a potential vulnerability for a particular repository.
Projects SHOULD host a `SECURITY.md` file in the root directory of their GitHub repository, alongside `README.md` and `LICENSE`.
This ensures high visibility and automatic integration with GitHub's security features.

Use the [SECURITY.md template](../SECURITY.md) from this repository as a starting point for your project.

## Recognition

The Pulp project may thank security researchers who help improve Pulp, through recognition in:

- Security advisories
- [Pulp Discourse](https://discourse.pulpproject.org)

## Policy updates

This policy may be updated periodically.
Suggestions for improvement can be submitted through issues or pull requests to the [pulp/governance](https://github.com/pulp/governance) repository.

## Notes

The key words "MUST", "MUST NOT", and "SHOULD" in this document are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119.html).
