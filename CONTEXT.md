# thoughtbot/factory_bot context
> refreshed 2026-09-03 | upstream default: main @ 18ae8b5

## Identity & policies
- upstream: thoughtbot/factory_bot, default branch `main`, primary language Ruby, English-first (yes — all docs/README in English)
- CLA/DCO: none (CONTRIBUTING has no CLA/DCO/signup requirement)
- AI-assisted PR policy: unstated (no AI disclosure requirement found)
- signed commits required: no (no branch protection on main)
- PR template: none (no PULL_REQUEST_TEMPLATE in repo or thoughtbot/.github) — use pipeline fallback body
- external tracker: github

## Conventions (verified from merged PRs)
- branch naming: mixed — `fix/typos`, `issue-1825`, `no-ruby2-keywords`, `nc/...`, `claude/...`; no dominant pattern. Use `fix/<kebab>`.
- commit style: plain imperative, no Conventional Commits
- test command: `bundle exec rake` (full suite + standard lint); `bundle exec rake all_specs` in CI
- CI: GitHub Actions `build.yml` (Ruby x Rails matrix, `bundle exec rake all_specs`) + `standard` job (`bundle exec rake standard`)
- CONTRIBUTING explicitly welcomes trivial fixes: "no patch is too small: fix typos, add comments, etc."
- outside PRs get merged: yes, responsive (recent external merges: #1830, #1828, #1824, #1823, #1819, #1818, #1816, #1815, #1814, #1795, #1794, #1793)

## Maintainer picture
- active maintainers: thoughtbot team; recent external contributors merged quickly (days)
- areas in flight: release automation (neilvcarvalho), internal refactors

## Issue-area health
- no contested/redesign signals relevant to trivial doc/typo work

## Gap ledger (dedupe — READ FIRST, never re-pick)
- 2026-09-03 trivial/minor-fix pass (loop-trivial) — outcome: see tried-repos.jsonl

## Mined gaps (discovered, not yet attempted)
- none yet
