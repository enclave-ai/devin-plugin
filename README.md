# Enclave for Devin

[Enclave](https://enclave.ai) is a fleet of autonomous security agents. They map your repositories and cloud into a live security graph, then hunt for vulnerabilities, run penetration tests and review pull requests the way a security researcher would. They verify reachability and exploitability before anything reaches your team.

This plugin brings that work into Devin. Devin sees the same verified findings, exploit context and security posture that Enclave's agents work from, and it can act on them in your codebase:

- **Fix verified findings** from security hunts, penetration tests, workflows and security chat, using the finding's summary, impact and proof of concept
- **Triage findings** against your actual code, marking them verified, resolved or invalid with a recorded reason
- **Summarize your security posture**: findings by severity and status, connected repositories and PR scan coverage
- **Check a pull request** before you merge, with Enclave's scan status, gate result and every flagged concern

## What's included

| Component | Name | What it does |
| :-- | :-- | :-- |
| MCP server | `enclave` | Connects to `https://mcp.enclave.ai` over Streamable HTTP with OAuth |
| Skill | `enclave-security-overview` | Snapshot of open findings, repositories and PR scan coverage |
| Skill | `enclave-fix-finding` | Fix a finding, add a regression test, then resolve it with your approval |
| Skill | `enclave-pr-security` | Enclave's security analysis for the current or a given PR |
| Skill | `enclave-triage-findings` | Check findings against the code and update their status with your approval |

### MCP tools

| Tool | Description |
| :-- | :-- |
| `list_orgs` | Organizations you can access |
| `list_findings` | Findings, filtered by status, severity or text, with pagination |
| `get_finding` | Full details of a finding. The proof of concept is shown only for verified findings |
| `get_pull_request_security` | Scan status, gate result and concerns for a PR (`<repo-slug>#<number>`) |
| `update_finding` | Set a finding's status (`verified`, `resolved`, `invalid`, `discarded`) with a reason |
| `get_org_security_snapshot` | Finding counts by severity and status, repositories, PR scan coverage |

## Setup

1. In Devin, open **Settings → Marketplace**, find **Enclave** and install it.
2. The first time a session uses the `enclave` MCP server, Devin asks you to authorize it. Sign in to Enclave and approve access. No API key is needed.
3. Ask Devin something like:
   - "What has Enclave found in this repo?"
   - "Fix the critical Enclave findings."
   - "Is my PR safe to merge according to Enclave?"
   - "Triage our unverified Enclave findings."

You need an Enclave account with at least one connected repository. [Get started](https://app.enclave.ai).

## Security and privacy

- The plugin is only Markdown skills and an MCP configuration that points at Enclave's hosted server. It ships no binaries and runs no local code.
- Access is scoped to the Enclave organization and repositories your account can see.
- Skills ask for your confirmation before they change a finding's status. Every change is recorded in your organization's Enclave activity timeline.
- Finding and PR text is treated as untrusted data, and proofs of concept are never run against external systems.

Documentation: [app.enclave.ai/docs/mcp](https://app.enclave.ai/docs/mcp). Report security issues to [support@enclave.ai](mailto:support@enclave.ai).

## Developing locally

```sh
git clone https://github.com/enclave-ai/devin-plugin
devin plugins install --local ./devin-plugin
```

Start a new `devin` session and ask it to use one of the Enclave skills. In Devin Cloud, install it from **Customize → Plugins → Add plugin → From repository** instead.

## License

[MIT](LICENSE)
