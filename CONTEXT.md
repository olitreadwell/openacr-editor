# GSA/openacr-editor context
> refreshed 2026-09-05 | upstream default: main @ c0238a76101fc0f46954f1879c94b9b4e839285f

## Identity & policies
- upstream: GSA/openacr-editor, default branch main, primary language Svelte (Vite + Svelte 5 legacy mode), English-first (yes — all UI/docs English).
- CLA/DCO: none (no CLA bot, no DCO, no contributor signup in CONTRIBUTING).
- AI-assisted PR policy: unstated (no AI/LLM/generated/Copilot/ChatGPT mention in repo CONTRIBUTING or org GSA/.github — org .github absent).
- signed commits required: no (no branch protection on main exposed via API).
- PR template: none (no .github/PULL_REQUEST_TEMPLATE.md, no root template, no org default). Fallback 3-section body.
- external tracker: GitHub.

## Conventions (verified from merged PRs)
- branch naming: no dominant pattern (2026-04-30-patch_workflow-permissions, OGPWEB-18758, RITM1278621, feature/icon_test, prod, staging, mgifford-patch-1). Fallback `fix/<kebab-description>`.
- commit style: plain imperative ("Text spacing fix", "Minor typo fix", "Migrate app to Vite and Svelte 5 legacy mode").
- test command: `npm test` (Cypress e2e, headless chrome), `npm run build`, `npm run a11y-test` (pa11y-ci).
- CI checks that gate merge: main.yml (build + deploy to gh-pages), a11y.yaml (pa11y), cypress.yaml (e2e), pre-commit.yaml (pre-commit hooks).
- how outside PRs get merged: responsive-ish; recent merges Apr 2026 (#85, #86 by drewnielson). Older external merges from mgifford, dmundra. Slow cadence (months between merges).

## Maintainer picture
- active maintainers: drewnielson (most recent, Apr 2026), yogitabholwankar, attorri, istankevychgsa, HarikaMunipalle, dmundra, mgifford.
- response latency: slow; issues sit for months without maintainer comment.

## Issue-area health
- 4 open issues, none maintainer-engaged:
  - #82 special chars in product name break download (2025-05-07, no comments) — real bug, not maintainer-engaged.
  - #81 add code.json (2025-04-25, no comments) — feature request.
  - #72 add 2.5 report type/catalogs (2024-10-18) — claimed by open PR #72 (toro-bah).
  - #58 preserve visually hidden text in license link (2024-01-03) — maintainer mgifford commented "This looks good" but claimed by open PR #58 (thibaudcolas, dirty/conflicted).
- No maintainer-engaged open issue survives (the engaged ones are claimed by open PRs) -> repo-audit matrix.

## Gap ledger (dedupe — READ FIRST, never re-pick)
- (first run — no prior attempts)

## Mined gaps (discovered, not yet attempted)
- 2026-09-05 clean-code `removeCriteria` in src/utils/updateEvaluation.js uses `if (criteriaIndex)` which is truthy for -1 and falsy for 0. When a criteria to remove is NOT present, findIndex returns -1 and splice(-1,1) removes the LAST criteria (wrong one); when the criteria is at index 0 it is not removed. Repro: node script simulating catalog switch to WCAG 2.0 with a missing 2.1-only criteria removes 4.1.2. Dedupe: no upstream issue/PR (searched "remove criteria", "catalog switch", "filename"). Fix: `if (criteriaIndex !== -1)`. — status: done — fork PR https://github.com/olitreadwell/openacr-editor/pull/2 (2026-09-05, CI green)
