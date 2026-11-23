# Full Signal Echo specification

## Product and delivery scope

Signal Echo helps people spot online scams, decide what to do next, and pass reliable warnings to others. Launch the responsive personal site and Android application first. Keep the consumer experience separate from the corporate workflow inside iot.EraX Console.

Spain is the initial jurisdiction. Start with suspicious bank notices and delivery messages received through SMS or WhatsApp. Locales determine presentation. The jurisdiction determines official advice, reporting destinations, and retention rules. An interface translated into a language does not extend jurisdiction coverage.

## Repository map

| Local path inside this hub | Repository owner | Delivery |
| --- | --- | --- |
| `frontend/signalecho-app` | [signalecho-app](https://github.com/Signal-Echo-Security/signalecho-app) | Personal React web experience and Android shell. Prepare iOS after Android qualification. |
| `microservices/api-signalecho` | [api-signalecho](https://github.com/Signal-Echo-Security/api-signalecho) | Product API, case use cases, policies, persistence and governed integrations. |
| `libs/signalecho-lib-contracts` | [signalecho-lib-contracts](https://github.com/Signal-Echo-Security/signalecho-lib-contracts) | Transport-neutral exceptions, locale metadata and shared public contracts. |
| `terraform/signalecho-terraformer` | [signalecho-terraformer](https://github.com/Signal-Echo-Security/signalecho-terraformer) | Terraform roots, cloud resources, remote state and change evidence. |

The hub owns this specification and architecture decisions. Nested checkouts retain their own Git remotes, issues, lockfiles and review workflows. Use the [Signal Echo project](https://github.com/orgs/Signal-Echo-Security/projects/1) for the owning issues. Create separate owners only when a new domain or a deployment boundary warrants one.

## Architecture and toolchain

- Reference the Hub Platform folder organization, issue-driven delivery, hexagonal services, CustomExceptions and localization conventions. Use TypeScript, Node.js 26, React, and Yarn 4 strict Plug’n’Play. Pin supported versions and commit lockfiles.
- Personal web and Android share the responsive React UI. Use Tauri 2 as the initial native container, preserving the independent Vite build and Yarn Plug’n’Play. Keep device-specific capabilities in the shell and thin adapters. The Vite 8 production build is verified under Plug’n’Play, and Vite warns that it does not actively maintain PnP-specific fixes. Recheck this compatibility when updating the lockfile. Expo’s documented Yarn setup needs the node-modules linker, and Capacitor’s native sync resolves platform dependencies from node_modules. For Android qualification, verify signed builds, browser return links, sharing, accessibility and device permissions. Reuse the web build and implement the platform-specific integration and store validation for iOS in a later phase.
- The NestJS API separates domain, application use cases and ports, adapters and framework composition. Business rules live with the owning application and domain. The API maps typed transport-neutral errors to a safe, versioned problem response at one boundary. Cross-library contracts carry stable codes, module, localization key, safe arguments, category and optional safe details.
- Start with one independent PostgreSQL datastore for reports, warnings and audit history. Evaluate JSONB for legitimately variable incident metadata. Decide persistence, messaging and specialized service splits through recorded requirements. Use additive contracts and isolation tests for any shared infrastructure.
- Publish dependencies for clean CI and external clones before release. The initial local workspace can use Yarn portals for independently checked-out sibling libraries. Keep private iot.EraX packages out of public installs. First-party service adapters should target approved versioned contracts across organizational boundaries.

## Personas, data and authorization

| Actor and channel | Authentication and scope | Data ownership |
| --- | --- | --- |
| Visitor on the personal site or app | Anonymous. Short-lived, rate-limited check context. | Submitted text is ephemeral by default. |
| Signed-in person on the personal site or app | Personal session issued through the iot.EraX identity authority. | Personal Signal Echo case and explicit sharing choices. |
| Corporate member in iot.EraX Console | Canonical Company and entitlement from Platform. Verify membership and delegated permissions for every effective company context. | Company incidents scoped by canonical companyId. |
| Moderator | Authorized scoped role, least-privilege view and audit record. | Review and redaction decisions for publishable warnings. |
| Maya and Storm Harbor service integrations | Separate service identity, scoped authorization and auditable calls. | Maya receives minimal input. Recovery evidence excludes case content. |

### Identity integration

1. Use the existing api-auth personal provider flow and maintained GitHub, LinkedIn and Google adapters. Verify approved callback and client contracts in the owning service before integration. Keep provider credentials and orchestration under api-auth.
2. Use the system browser and a validated return link for native sign-in. Bind the OAuth state and PKCE proof to the attempt. Use the approved secure session storage design. For web, use the approved same-origin session/BFF pattern and secure browser cookies.
3. Add corporate capabilities as a module in iot.EraX Console through the owning Platform repository and issue. Use api-foundation for canonical Company, membership and entitlements. Use versioned APIs and scoped access. Signal Echo owns incident rules. A corporate administrator’s access is scoped to authorized company incidents.
4. Apply independent tests for person, Company, participant and moderator authorization. Require explicit user action for any sharing across contexts and record consent and purpose.

## Privacy and anonymity by default

- Allow a person to read official guidance and make the initial check without an account. Keep raw submissions out of persistent storage, telemetry and logs by default. Avoid advertising trackers, analytics identifiers and session replay in the pilot.
- Minimize input before any Maya or provider call. Remove personal identifiers and unique links when possible. If the remaining content still presents undue identification risk, keep the external call disabled for that input and offer the official guidance.
- Publish only patterns that pass review for re-identification risk. Remove names, contacts, screenshots, case IDs and combinations of details that could identify a person or company. Public warnings link to guidance and patterns, never to the source case.
- Treat saved cases, sign-in records and any identifiable security telemetry as personal data. Use purpose-specific access and retention controls. Review the processing grounds, transparency, retention, data subject rights and any provider transfers before the pilot accepts identifiable data.
- Use synthetic fixtures for development, tests and Storm Harbor exercises. Assess anonymity in context. Removing direct identifiers alone does not establish anonymization.

## Localization and accessibility

Match the 25 locale distinctions in the Harbor Lens catalog. Use RTL for `ar`, `he-IL` and `ur-PK`. Preserve the complete list in the shared contracts package and reconcile any changes to the Harbor Lens reference.

`en-GB`, `en-US`, `es-ES`, `ca-ES`, `pt-PT`, `pt-BR`, `it-IT`, `ru-RU`, `de-DE`, `fr-FR`, `uk-UA`, `et-EE`, `pl-PL`, `bg-BG`, `zh-Hans`, `hi-IN`, `ja-JP`, `he-IL`, `ur-PK`, `af-ZA`, `ar`, `ko-KR`, `tr-TR`, `id-ID`, `vi-VN`.

- Set document language and direction and use CSS logical properties. Preserve appropriate direction for pasted mixed-language material, URLs, numbers and technical identifiers.
- Use stable translation keys for all visible text and error messages. Verify key and interpolation parity, plural rules, locale selection and text expansion. Review safety-related translations before release.
- Test navigation, reading order, focus, contrast and screen-reader labels on desktop and Android. The initial native and web shells share catalog ownership.

## Delivery phases and acceptance

### 1. Workspace and executable foundations

- Set up repositories, project metadata, branch protections and local checkouts.
- Deliver the web frontend first for review. Include the first React page, shared locale contract and RTL behavior. Keep the preview free of sign-in prompts, reporting forms and analytics.
- Use the web review to confirm navigation and product language before publishing backend and Android implementation work. Then qualify the NestJS hexagonal composition, health and readiness endpoints and the Tauri shell.
- Exit evidence for the initial web review: production web build, package checks, exact Harbor Lens locale parity and a local preview. Native packaging and service integration have their own validation gates.

### 2. Anonymous check and official guidance

- Let a visitor paste message text and select the situation. Minimize or redact data before Maya. Apply request size and rate limits, treat messages as untrusted input, and keep quick checks ephemeral.
- Ask Maya for explained signs with uncertainty and safe structured results. When Maya is unavailable, show the reviewed next steps. Avoid definitive fraud verdicts based solely on model output.
- Maintain source-linked official Spanish guidance for a suspicion, credentials shared, and money already sent. Record source, jurisdiction, review date and owner.
- Exit evidence: safe guidance works during an AI outage. Synthetic cases demonstrate redaction, bounded inputs, source links and no retention for anonymous checks.

### 3. Personal sessions and private cases

- Integrate GitHub, LinkedIn and Google through api-auth. Verify identity linking, session expiry, mobile browser return and recovery from failed sign-in.
- Allow a person to explicitly save or delete a case and export a reviewable incident summary. Keep formal reporting in the named official channel. Use idempotency for report creation and transitions.
- Exit evidence: identity journeys, tenant isolation, retention/deletion and export authorization pass with synthetic data.

### 4. Reviewed community warnings

- Allow authorized submissions and moderation. Publish a redacted description and practical warning only after review. Preserve source and uncertainty, correct stale warnings and deduplicate patterns.
- Avoid publishing raw personal identifiers or treating a sender identifier as proof. Make abuse reporting and correction possible.
- Exit evidence: moderation, deduplication, redaction, takedown and share behavior pass, including RTL.

### 5. Corporate module in iot.EraX Console

- Define integration contracts with the Console, its BFF, api-auth and api-foundation before changing their repositories. Use approved Company context and scoped roles.
- Allow authorized company users to record company incidents, review risk patterns and export authorized reports. Audit data access and state transitions.
- Exit evidence: authorized company workflows and cross-company denial prove the corporate boundary. Personal case data stays scoped to its owner.

### 6. Infrastructure, reliability and Android release

- Use Terraform and Kubernetes. Evaluate DigitalOcean for the first environment. Decide the managed database placement, private network, encrypted backup, state and credential scheme in the Terraform repository.
- Add build provenance, metrics/traces without case content, deploy and rollback checks. Use a portable encrypted copy in a separate failure domain and rehearse restore before handling real pilot reports.
- Validate Android SDK and NDK builds, installation, signed distribution, accessibility, OAuth return and share behavior on supported devices.
- Use Storm Harbor to restore the application and a previously confirmed synthetic report in another cloud. Check URL, availability, duplicate prevention and measurable RTO/RPO. Send only operational evidence to Harbor Lens.
- Exit evidence: approved pilot, recoverable site, accepted security and privacy review, and tested Android build. Complete the repository license decision before releasing code.

### 7. iOS and expansion

- Add an iOS native target to the same client after validating signing, universal links, secure storage, sharing and App Store requirements. Retain the shared UI and contracts.
- Extend jurisdiction coverage as reviewed official guidance and applicable reporting channels become available. Evaluate EU funding using pilot evidence and the conditions of the applicable call.

## References

- [Tauri mobile prerequisites](https://v2.tauri.app/start/prerequisites/)
- [Tauri with Vite](https://v2.tauri.app/start/frontend/vite/)
- [Expo package manager compatibility](https://docs.expo.dev/more/create-expo/)
- [Capacitor native package resolution](https://github.com/ionic-team/capacitor/blob/main/ARCHITECTURE.md)
- [GDPR, including Recital 26 and Articles 5 and 25](https://eur-lex.europa.eu/eli/reg/2016/679)
- [AEPD data protection by default](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/proteccion-de-datos-por-defecto)
- [AEPD on anonymized information](https://www.aepd.es/preguntas-frecuentes/0-conceptos-basicos/FAQ-0005-sobre-los-datos-anonimizados)
