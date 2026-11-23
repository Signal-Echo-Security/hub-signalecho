# Signal Echo repository guidance

## Scope

Signal Echo is maintained by Signal Echo Security. The first release focuses on Spanish-language guidance for suspected and confirmed online scams in Spain. The first scenarios are fake bank notices and fake delivery messages received by SMS or WhatsApp.

## Product decisions

- The personal experience is the Signal Echo site and Android app, with iOS to follow. It starts with guidance for suspicious bank and delivery messages in Spain.
- Personal sign-in uses the iot.EraX identity authority and its GitHub, LinkedIn and Google providers. Corporate Signal Echo journeys live in iot.EraX Console with canonical Company scope and entitlements.
- Review the personal web frontend first. Keep guidance and initial checks anonymous by default. Keep identifiable saved reports private and publish only anonymized patterns.
- Follow Harbor Lens locale parity and RTL in the user interface. Keep CustomExceptions transport-neutral, use hexagonal backend boundaries and share cross-project contracts through the owned library.
- The [full Signal Echo specification](./SPECS-FULL-SIGNAL-ECHO.md) owns the delivery plan and integration acceptance criteria. Track owning issues in the [Signal Echo GitHub Project](https://github.com/orgs/Signal-Echo-Security/projects/1).

## Repository boundaries

- Use `hub-platform` as the reference for root hub architecture, issue-driven delivery, and shared TypeScript conventions. Adopt conventions that suit Signal Echo and keep its configuration and dependencies independently maintainable.
- Keep product and architecture decisions, shared application contracts, and integration boundaries in this hub. Manage cloud resources through [signalecho-terraformer](https://github.com/Signal-Echo-Security/signalecho-terraformer) and link work through the respective owning issues.
- Use the governed Maya API for consultative analysis. Maintain authorization, auditability, provider portability, and data minimization across the API boundary.
- Coordinate recovery exercises with [Storm Harbor](https://github.com/Storm-Harbor/storm-harbor-control-plane). Signal Echo supplies the workload, synthetic fixtures, and restore checks. Harbor Lens can receive operational evidence without incident content.

## GitHub workflow

- Keep `develop` as the default integration branch and `master` as the production baseline. Base issue branches on the current `origin/develop` and target `develop` in implementation pull requests. Promote validated `develop` to `master` in a separate pull request.
- Open the owning issue before branching. Use the GitHub issue number in `<issue-number>-feat-<slug>` or `<issue-number>-fix-<slug>`. Use the appropriate native issue type and keep project metadata current when a Signal Echo project board is configured.
- Write repository-facing material in English, with localized user-facing content where applicable. Use Conventional Commits, link the owning issue, and document the scope, validation, and deployment impact in the pull request.
- A maintainer reviews and merges manually after resolving discussions and reviewing validation. Each dependent repository follows the branch policy documented in its own `AGENTS.md`.

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
