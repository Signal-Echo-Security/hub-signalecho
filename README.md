# Signal Echo

Signal Echo is a project to help people spot online scams, decide what to do next, and share warnings that help others.

This is the root hub for Signal Echo product architecture, engineering documentation, and integration contracts. The application is in development.

## First release

The first release is planned for Spain, with a Spanish-language site that works on mobile. It will start with fake bank notices and fake delivery messages sent by SMS or WhatsApp.

- **Check a suspicious message.** Maya will explain the warning signs and make uncertainty clear. The initial check is designed to work without an account.
- **Find the next step.** Read practical guidance drawn from official sources. The guidance will remain available if Maya is unavailable.
- **Prepare a private incident summary.** Organize what happened, review the summary and export it for use with the appropriate official channels.

## Technical direction

The stack uses TypeScript, Node.js 26, React, and Yarn Plug’n’Play. Kubernetes and Terraform support reproducible deployments. DigitalOcean is the first deployment target under evaluation, with PostgreSQL proposed as the initial datastore.

Signal Echo will also provide a reference workload for Storm Harbor. The first recovery exercise will use synthetic data to restore the site and its data in a second cloud, confirm the public URL and a saved incident report, and measure recovery time and data loss.

## Repository and integration ownership

| Owner | Responsibility |
| --- | --- |
| **hub-signalecho** | Product scope, reference architecture, implementation roadmap, and cross-repository decisions. |
| [**signalecho-terraformer**](https://github.com/Signal-Echo-Security/signalecho-terraformer) | Terraform modules, cloud environment configuration, and infrastructure change records. |
| **Maya** | Consultative analysis through its governed API. Signal Echo owns the user flow, data minimization, and official guidance. |
| [**Storm Harbor**](https://github.com/Storm-Harbor/storm-harbor-control-plane) | Recovery exercises and evidence collection. Signal Echo supplies the reference workload and verification criteria. |

## Delivery workflow

Open an issue and create an issue branch from `develop`. Submit the pull request to `develop` and record validation. A maintainer reviews and merges it manually. Production promotion goes from validated `develop` to `master` in a separate pull request.

Infrastructure changes follow the Terraform repository’s issue-to-`master` workflow and manual apply approval.

## Contributing

Use [GitHub Issues](https://github.com/Signal-Echo-Security/hub-signalecho/issues) for product ideas and implementation proposals. See [AGENTS.md](./AGENTS.md) for repository conventions. The project is intended to be open source. The license will be selected before code is released.
