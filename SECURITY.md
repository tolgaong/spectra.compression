# Security Policy

## Reporting a vulnerability

Do not disclose an unpatched vulnerability, exploit details, credentials, or a
sensitive archive in a public issue.

Use this repository's GitHub **Report a vulnerability** / private security
advisory path when it is available. If private reporting is unavailable, open a
minimal public issue asking the maintainer to establish a private reporting
channel. Include no sensitive technical details or attachments in that issue.

For ordinary malformed-input failures or compatibility bugs that are safe to
discuss publicly, use the bug-report form and provide the smallest non-sensitive
reproduction possible.

## Scope and handling

Useful reports identify the affected package and version, runtime and operating
system, input format, API shape, observed impact, and whether limits or safe
path policies were enabled. Reports involving path traversal, excessive CPU or
memory use, decompression bombs, validation bypass, secret exposure, or
incorrect integrity results are security-relevant.

No response-time or remediation SLA is implied. Reports are prioritized by
risk, correctness impact, affected usage, blast radius, and workaround
availability.
