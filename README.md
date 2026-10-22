# Awesome-Notification-Infrastructure

# Top Notification Infrastructure Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Multi-Channel Routing, In-App Inboxes & Self-Hosted Data Ownership*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Notification Infrastructure**. These tools provide the routing, templating, preference management, and delivery observability layer between your application and the providers that actually send messages — so you trigger one event and the platform handles the fan-out to email, SMS, push, chat, and in-app inbox.

**Examples** include Novu, Courier, Knock, OneSignal, Twilio SendGrid, Postmark, AWS SES, and Braze (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, multi-channel fan-out, and transparent delivery logic — ideal for teams who want notification data and workflows on their own infrastructure rather than per-event SaaS pricing.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **Courier** — Notification infrastructure API with a visual template designer, user preference management, and a drop-in inbox component. **Idempotency keys supported on `POST /send`**, with responses replayed for 25 hours by default and up to one year with `x-idempotency-expiration` [citation:4]. **Message statuses include `UNROUTABLE`, `UNDELIVERABLE`, and `UNMAPPED`** for diagnosing why a notification failed to reach a provider or template [citation:4]. Official SDKs for Node.js and Python with typed requests and automatic retries (up to 2 times with exponential backoff) [citation:9][citation:14]. **Best for teams wanting polished template design and inbox UI** without building the infrastructure.

- **Knock** — Developer-focused notification orchestration platform built around **workflows that react to events rather than direct send calls**. You publish an event (e.g., `user_created`), and the workflow executes conditional logic, delays, and channel steps based on the recipient's profile data [citation:3]. **Timestamp-based scheduling** uses a user's actual `created_at` rather than "now + X days," enabling precise onboarding sequences [citation:3]. **Best for event-driven notification logic** that needs to react to user state changes.

- **Twilio SendGrid** — The reference email delivery API with high deliverability, dynamic templates, and webhook event tracking. **Best for teams needing email as the primary channel** with a provider they already trust.

- **Postmark** — Transactional email provider known for fast delivery and clean API design. **Best for transactional emails** where speed and inbox placement matter.

- **OneSignal** — Push notification and in-app messaging platform with a generous free tier and multi-platform SDKs. **Best for mobile-first products** needing push without building APNs/FCM infrastructure.

## Open-Source GitHub Projects

- **[Novu](https://github.com/novuhq/novu)**  
  **The leading open-source notification infrastructure** — MIT licensed, **36,814+ GitHub stars** [citation:2]. **A self-hosted alternative to Knock, Courier, and OneSignal that you fully own** [citation:1]. **Send transactional and product notifications across email, SMS, push, chat, and a drop-in in-app inbox from a single API and a visual workflow editor** [citation:1]. **Built-in subscriber management, preferences, digests, and provider routing** [citation:1]. **Architecture**: NestJS API, Bull/Redis-backed worker for workflows and digests, WebSocket service for real-time in-app delivery, React dashboard for workflow building, backed by MongoDB and Redis [citation:1]. **In-app notification center** ships as `@novu/react` with `<Inbox />`, `<Bell />`, and `<Preferences />` components — WebSocket updates, reconnection, pagination, and mark-as-read handled automatically [citation:11]. **SDKs** for Node.js, Python, PHP, .NET, Go, Java, Ruby, and more [citation:2][citation:7]. **Self-hosting requires MongoDB 8 and Redis**, with your own provider credentials (SendGrid, Twilio, Firebase) added via the dashboard [citation:1][citation:6]. **Best for teams wanting a self-hosted, full-stack notification platform** with a visual workflow editor and drop-in inbox.

- **[Apprise](https://github.com/caronc/apprise)**  
  **The universal notification router** — MIT licensed, **16,700+ GitHub stars** [citation:15]. **A send-only library/CLI that normalizes one message out to ~143 upstream services** via `service://creds@host/target` URL syntax [citation:15]. **Not a push server** — it has no app and never receives anything; it sits a layer above ntfy and Gotify, dispatching to them as targets [citation:15]. **Apprise-API** wraps it as a REST microservice [citation:15]. **Best for fan-out to many providers** from a single interface — email, Slack, Discord, Telegram, Pushover, and dozens more.

- **[ntfy](https://github.com/binwiederhier/ntfy)**  
  **The HTTP-based pub-sub push server** — Apache 2.0/GPLv2 licensed, **30,700+ GitHub stars** [citation:15]. **Single Go binary**, ~20–50 MB footprint [citation:15]. **Own Android and iOS apps** — iOS push works via an APNs relay because Apple forbids background WebSocket connections [citation:15]. **Features**: priorities 1–5, emoji tags, attachments up to 15 MB, up to 3 action buttons, scheduled delivery via `X-Delay`, per-topic ACLs, and a **UnifiedPush distributor** for push without Google FCM [citation:5][citation:15]. **Best for self-hosted push notifications** where you want a full chain (REST publish → message store → mobile app) without cloud dependency.

- **[Gotify](https://github.com/gotify/server)**  
  **The minimal self-hosted push server** — MIT licensed, **15,100+ GitHub stars** [citation:15]. **One container, one `/app/data` volume holding SQLite**, seed admin password with `GOTIFY_DEFAULTUSER_PASS` [citation:5]. **Under 50 MB RAM** — runs on a Pi [citation:5]. **Deliberately leaner than ntfy**: `POST /message?token=<apptoken>`, optional title/priority, **no attachments, tags, or action buttons** [citation:5]. **Android app only** — no official iOS app [citation:15]. **Best for the easiest possible self-hosted push** on a homelab or small team.

### Additional Strong Open-Source Options

- **Dittofeed** — Open-source customer engagement platform with journey builder and event-triggered messaging across email, SMS, push, and in-app. MIT licensed. Positioned as a self-hostable alternative to Braze and Customer.io.
- **Listmonk** — Open-source newsletter and mailing list manager. Self-hosted with PostgreSQL, no per-subscriber pricing. Best for email-heavy notification workloads.
- **Postal** — Open-source mail server with a web UI for managing sends, domains, and tracking. Best for teams wanting to own the email delivery infrastructure entirely.

**Frameworks for building custom systems**: Combine **Novu** for a self-hosted full-stack notification platform with visual workflows and a drop-in inbox, **Apprise** for routing one message to 143+ providers, **ntfy** or **Gotify** for self-hosted push with mobile apps, and **Listmonk** or **Postal** for email-heavy workloads — to build a notification stack tailored to your channel mix, data ownership requirements, and operational appetite.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Notification infrastructure tools differ significantly in deployment model, channel coverage, and pricing philosophy. **Novu is the most complete open-source option** with a visual workflow editor, multi-channel fan-out, and a drop-in React inbox — but self-hosting requires MongoDB, Redis, and managing a multi-service architecture [citation:1][citation:6]. **Courier and Knock are managed SaaS** — Courier excels at template design and inbox UI with idempotency support [citation:4], while Knock excels at event-driven conditional workflows with timestamp-based scheduling [citation:3]. **Apprise is a router, not a push server** — it dispatches to services like ntfy and Gotify but has no app of its own [citation:15]. **ntfy solves iOS push via an APNs relay** because Apple forbids background WebSocket connections [citation:15]. **Gotify has no official iOS app** [citation:15]. **Self-hosting shifts operational responsibility to you** — provider credential storage, delivery retry logic, and preference enforcement become your code, not the vendor's.
- Self-hosted open-source solutions require proper database backups (MongoDB for Novu, SQLite for Gotify), Redis queue monitoring, and provider API key management.

---

**Made for backend engineers, product teams, and platform architects building notification systems they can own and control.**
Let's make notification infrastructure more open, multi-channel, and data-sovereign.
