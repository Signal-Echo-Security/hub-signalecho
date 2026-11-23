# Signal Echo

Signal Echo is a project to help people spot online scams, decide what to do next, and share warnings that help others.

This repository contains the initial product and engineering documentation. The application is in development.

## First release

The first release is planned for Spain, with a Spanish-language site that works on mobile. It will start with fake bank notices and fake delivery messages sent by SMS or WhatsApp.

- **Check a suspicious message.** Maya will explain the warning signs and make uncertainty clear. The initial check is designed to work without an account.
- **Find the next step.** Read practical guidance drawn from official sources. The guidance will remain available if Maya is unavailable.
- **Prepare a private incident summary.** Organize what happened, review the summary and export it for use with the appropriate official channels.

## Technical direction

The stack uses TypeScript, Node.js 26, React, and Yarn Plug’n’Play. Kubernetes and Terraform support reproducible deployments. DigitalOcean is the first deployment target under evaluation, with PostgreSQL proposed as the initial datastore.

Signal Echo will also provide a reference workload for Storm Harbor. The first recovery exercise will use synthetic data to restore the site and its data in a second cloud, confirm the public URL and a saved incident report, and measure recovery time and data loss.

## Contributing

Use [GitHub Issues](https://github.com/Signal-Echo-Security/hub-signalecho/issues) for product ideas and implementation proposals. See [AGENTS.md](./AGENTS.md) for repository conventions. The project is intended to be open source. The license will be selected before code is released.
