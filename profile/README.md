<div align="center">

<img src="https://raw.githubusercontent.com/dowl-io/.github/main/assets/dowl-logo.png" alt="Dowl" width="80" />

# Dowl

**Do. Weave. Learn.**

*The practice ground and hiring lens for integration engineers.*

[![Status](https://img.shields.io/badge/status-building-orange?style=flat-square)](#)
[![Stack](https://img.shields.io/badge/stack-Go%20·%20Next.js%20·%20Astro%20·%20DataWeave-teal?style=flat-square)](#)
[![Infra](https://img.shields.io/badge/infra-GCP%20·%20Kubernetes%20·%20Terraform-blue?style=flat-square)](#)

</div>

---

## What is Dowl?

Integration engineering is a craft. Like any craft, it only sharpens through deliberate, repeated practice — not tutorials, not videos, not reading documentation.

**Dowl** is where integration engineers go to sharpen their skills through real challenges with auto-validated test cases. Write the script. Run it. The test harness tells you the truth.

For engineers, it's a personal dojo — a place to grind through DataWeave transformations until the logic becomes instinct.

For companies, it's a proof layer — structured live assessments that show exactly what a candidate can build, not just what their resume claims.

> *The initials aren't an accident.*

---

## The Problem We're Solving

Most integration engineers pick up DataWeave on the job — piecing together answers from documentation fragments, Stack Overflow threads, and trial and error under deadline pressure. There is no structured path from beginner to fluent. No place to sit with a hard problem and work it through until the skill becomes second nature.

And when companies hire for integration roles, they're flying blind. A certification says someone studied. It doesn't say they can transform a deeply nested JSON payload under time pressure without Googling every operator.

There is no LeetCode for DataWeave. Dowl fills that gap.

---

## Who It's For

**Integration engineers** at any level who want to move from knowing DataWeave to *owning* it — whether preparing for a MuleSoft certification, levelling up in their current role, or sharpening craft for its own sake.

**Tech leads and hiring managers** at small and mid-cap companies who need a real signal when evaluating candidates for integration roles. Send a Dowl assessment, see what they actually build.

---

## Repositories

| Repo | Purpose | Stack |
|------|---------|-------|
| [`dowl-web`](https://github.com/dowl-io/dowl-web) | Public marketing site | Astro + TypeScript |
| [`dowl-docs`](https://github.com/dowl-io/dowl-docs) | Developer docs, API reference, challenge authoring guide | Starlight (Astro) + MDX |
| `dowl-app` *(private)* | Interactive IDE, challenge browser, hiring dashboard | Next.js 14+ · App Router · TypeScript |
| `dowl-api` *(private)* | Core backend — auth, scoring, challenge engine, assessment sessions | Go · Fiber · PostgreSQL · Redis |
| `dowl-runner` *(private)* | Sandboxed DataWeave script execution and test harness | Go · Docker · gVisor · DataWeave CLI |
| `dowl-challenges` *(private)* | Challenge content library — specs, test cases, difficulty tiers | YAML · JSON Schema |
| `dowl-shared` *(private)* | Language-agnostic API contracts — source of truth for all services | OpenAPI 3.1 |
| `dowl-infra` *(private)* | Infrastructure as code, CI/CD, secrets, environments | Terraform · GitHub Actions · GCP |
| [`.github`](https://github.com/dowl-io/.github) | Org-wide templates, contribution guides, org profile | — |

---

## How It Works

A candidate writes a DataWeave script in the browser. From there:

```
dowl-app → dowl-api → [GCP Pub/Sub] → dowl-runner
                                             ↓
dowl-app ← dowl-api ← [Redis result] ← execution output
```

The submission travels through a message queue, is picked up by an isolated runner pod, executed inside a Docker container with no network access and hard resource limits (CPU, memory, wall time), and the result is streamed back to the browser via Server-Sent Events. Every script runs as if it were hostile input. Because it might be.

---

## Architecture Principles

- **Strict separation of concerns** — 8 repositories, each with its own deployment cycle, access control, and security boundary
- **Language-agnostic contracts** — OpenAPI 3.1 specs in `dowl-shared` generate TypeScript types for the frontend and Go structs for the backend; no manual type drift
- **Defence-in-depth for execution** — `dowl-runner` is never exposed to the internet; scripts execute inside ephemeral containers with dropped Linux capabilities and a read-only filesystem; gVisor (`runsc`) runtime for enhanced kernel-level isolation on Kubernetes
- **Stateless, cloud-native** — containerised microservices targeting GCP; infrastructure reproducible via Terraform
- **Auth handled externally** — Clerk for JWT-based sessions and org-level multi-tenancy; no bespoke auth code in the MVP

---

## Status

Dowl is in active early development. We are building in private, validating the core execution pipeline with a small group of DataWeave practitioners, and working toward a public beta.

If you are a MuleSoft or DataWeave practitioner and want early access — or a company interested in piloting the hiring assessment tool — reach out.

---

## Get Involved

We are not open to general contributions yet. We are selectively looking for:

- **DataWeave challenge authors** — experienced integration engineers who want to contribute challenge specs and test cases to the content library
- **Early beta testers** — developers willing to use Dowl for real upskilling and give honest, unfiltered feedback
- **Frontend contributors** — once `dowl-app` opens, we will be looking for engineers comfortable with Next.js App Router and complex editor UIs

Watch this org to be notified when we open up.

---

## Contact

- 🌐 [dowl.io](https://dowl.io)
- 📧 [hello@dowl.io](mailto:hello@dowl.io)
- 💼 [LinkedIn](https://linkedin.com/company/dowl-io)

---

<div align="center">

*Do. Weave. Learn. Repeat.*

</div>
