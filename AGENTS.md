# Signal Echo repository guidance

## Scope

Signal Echo is maintained by Signal Echo Security. The first release focuses on Spanish-language guidance for suspected and confirmed online scams in Spain. The first scenarios are fake bank notices and fake delivery messages received by SMS or WhatsApp.

Use issues and reviewed pull requests for repository changes. Identify the owning issue, work on its branch, and record validation in the pull request. When the GitHub Project is configured, update the issue’s project metadata. Merge through the repository’s manual review process.

## Development

- Use TypeScript, Node.js 26, stable React, and stable Yarn with strict Plug’n’Play and no `node_modules`. Pin exact versions when introducing the toolchain. Follow the relevant Hub Platform conventions and reuse only dependencies compatible with public distribution.
- Validate untrusted JSON at API boundaries. Reuse versioned TypeScript contracts between the web app and backend where they serve both callers.
- Keep infrastructure reproducible with Terraform and portable Kubernetes manifests. Keep credentials and Terraform state out of Git. DigitalOcean is the first cloud under evaluation.
- PostgreSQL is the proposed first datastore. Use relational data for stable fields and JSONB when variation in report data justifies it. Evaluate another database only for a distinct use case.

## Privacy and guidance

- Treat pasted messages and incident reports as untrusted input. Keep quick checks ephemeral by default. Before sending text to Maya, minimize it and remove identifying details when possible. Keep report contents, credentials, and personal data out of telemetry and public fixtures.
- Use Maya as a consultative integration. Explain the signs that support an assessment and make uncertainty explicit. Keep reviewed guidance and links to official channels available independently.
- Keep incident reports private. Tell the user when an export is prepared for use with a formal reporting channel.

## Recovery

- Plan for encrypted backups and verify restoration with a portable database copy outside the first provider’s failure domain. Keep recovery credentials and keys accessible through the agreed recovery process.
- Start recovery exercises with synthetic data. Restore the application in another cloud, check the public URL and a previously confirmed report, and verify that repeated submissions do not duplicate reports. Record recovery time and observed data loss for Storm Harbor and Harbor Lens without including report contents.
