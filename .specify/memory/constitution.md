<!--
Sync Impact Report
- Version change: (template, unversioned) → 1.0.0
- Modified principles (placeholder → new title):
  - [PRINCIPLE_1_NAME] → I. Clean Code
  - [PRINCIPLE_2_NAME] → II. Simple UX
  - [PRINCIPLE_3_NAME] → III. Responsible Design
  - [PRINCIPLE_4_NAME] → IV. Minimal Dependencies
  - [PRINCIPLE_5_NAME] → V. No Automated Testing (NON-NEGOTIABLE)
- Added sections: Technology Stack Constraints, Development Workflow & Quality Gates, Governance
- Removed sections: none
- Deferred TODOs: none
- Note: Principle V intentionally overrides any test-related guidance in Spec Kit templates
  (plan/tasks/checklists); dependent artifacts MUST omit test tasks at generation time.
-->

# next-speckit-test Constitution

## Core Principles

### I. Clean Code

- Code MUST be readable first: descriptive names, small focused functions and components,
  and a single clear responsibility per module.
- Code MUST be written in TypeScript with strict typing; `any` MUST NOT be used without an
  inline justification.
- Dead code, commented-out code, and unused exports MUST be removed before merge.
- Duplication MUST be eliminated once a pattern appears three times; abstractions MUST NOT be
  introduced speculatively (YAGNI).
- `npm run lint` MUST pass with zero errors.

Rationale: With no automated tests (Principle V), readability and static checks are the
primary safeguards of correctness.

### II. Simple UX

- Every screen MUST serve one primary task with one obvious primary action.
- UI MUST use plain language, consistent layout, and predictable navigation; hidden or
  gesture-only interactions MUST NOT be the sole way to reach a feature.
- Features MUST NOT add settings, options, or steps unless a concrete user need is documented
  in the feature spec.
- Loading, empty, and error states MUST be explicitly designed for every user-facing view.

Rationale: Fewer choices and clear states reduce user error and support burden.

### III. Responsible Design

- UI MUST meet WCAG 2.2 AA: semantic HTML, keyboard operability, visible focus, sufficient
  color contrast, and text alternatives for non-text content.
- Personal data MUST be collected only when required by a documented feature need, and MUST
  NOT be logged or exposed to the client unnecessarily.
- Security practices MUST follow the OWASP Top 10: validate input at system boundaries, never
  trust client data, and keep secrets out of client bundles and source control.
- Pages MUST favor server rendering and minimal client JavaScript to respect user bandwidth,
  device constraints, and energy use.
- Dark patterns (deceptive defaults, forced continuity, confirm-shaming) are prohibited.

Rationale: The product MUST be accessible, safe, and respectful of its users by default.

### IV. Minimal Dependencies

- New runtime or dev dependencies MUST NOT be added when the need can be met by the platform
  (Web APIs), Next.js, React, Tailwind CSS, or a small amount of in-repo code.
- Any proposed dependency MUST be justified in the feature plan with: purpose, alternatives
  considered, bundle-size impact, maintenance status, and license.
- UI component libraries, CSS-in-JS libraries, and state-management libraries MUST NOT be
  added; styling uses Tailwind CSS and state uses React primitives.
- Unused dependencies MUST be removed promptly.

Rationale: Each dependency adds attack surface, upgrade cost, and bundle weight.

### V. No Automated Testing (NON-NEGOTIABLE)

- The project MUST NOT contain unit tests, integration tests, or end-to-end tests.
- Test frameworks and tooling (e.g., Jest, Vitest, Testing Library, Playwright, Cypress) MUST
  NOT be installed or configured, and a `test` script MUST NOT be added to `package.json`.
- Specs, plans, tasks, and checklists MUST NOT include test-writing tasks, TDD steps, or
  test-coverage gates.
- This principle supersedes any other guidance, template, command, or convention that
  requires or recommends tests, including default Spec Kit templates.

Rationale: Explicit project decision; quality is ensured through type checking, linting,
build verification, and manual review instead.

## Technology Stack Constraints

- The stack is fixed to the exact versions declared in `package.json`:
  - `next` 16.4.6 (App Router, `app/` directory)
  - `react` 19.3.0 and `react-dom` 19.3.0
  - `tailwindcss` 4.3.3 and `@tailwindcss/turbopack` 4.3.3
  - `eslint-config-next` 16.4.6, TypeScript 5
- These versions MUST NOT be upgraded, downgraded, or replaced without a constitution
  amendment.
- Code MUST use APIs and conventions valid for these exact versions. Because this Next.js
  version contains breaking changes, the bundled docs in `node_modules/next/dist/docs/` MUST
  be consulted before writing Next.js code, and deprecation notices MUST be heeded.
- Alternative frameworks, rendering libraries, or styling systems MUST NOT be introduced.

## Development Workflow & Quality Gates

- Every change MUST pass these gates before merge: `npm run lint` (zero errors), TypeScript
  type checking with no errors, and a successful `npm run build`.
- User-facing changes MUST be manually verified in the browser via `npm run dev`, including
  keyboard navigation and loading/empty/error states.
- Code review MUST confirm compliance with Principles I–V and the Technology Stack Constraints.
- Feature work follows the Spec Kit flow (specify → plan → tasks → implement), with all
  generated artifacts conforming to this constitution.

## Governance

- This constitution supersedes all other practices, templates, and guidance in this
  repository. Where conflicts arise, this document wins; Principle V takes precedence over
  any conflicting guidance.
- Amendments MUST be made via `/speckit-constitution`, documented in the Sync Impact Report,
  and approved by the project maintainer before merge.
- Versioning follows semantic versioning:
  - MAJOR: backward-incompatible removal or redefinition of a principle or constraint.
  - MINOR: new principle or section, or materially expanded guidance.
  - PATCH: clarifications, wording, or typo fixes.
- Compliance MUST be verified during every code review and in each feature plan's
  Constitution Check; unjustified violations block merge.
- Runtime agent guidance lives in `AGENTS.md` and MUST remain consistent with this document.

**Version**: 1.0.0 | **Ratified**: 2026-11-25 | **Last Amended**: 2026-11-25
