# thoughtbot/factory_bot context
> refreshed 2026-09-24 | upstream default: main @ 18ae8b5 (unchanged)

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
- 2026-09-03 trivial/minor-fix pass (loop-trivial) — PR #1 opened (fix/docs-cleanup): 7 genuine doc fixes (Factory.define->FactoryBot.define x2, missing `do`, callback counts 4->7 and 6->7, missing comma x2). 2 dead links found but left unfixed (no replacement URL).
- 2026-09-09 trivial/minor-fix pass (loop-trivial) — PR #2 opened (fix/typo-cleanup): 4 genuine typo fixes (SECURITY.md "the the", register_strategy.md `initalize_with`, rewinding.md `factoryBot.rewind_sequence`, REPRODUCTION_SCRIPT.rb "reproduct"). GETTING_STARTED.md "four callbacks" verified CORRECT (its list has 4) — do not re-fix.
- 2026-09-24 engine/loop (ANY repo) — PR #3 opened (fix/aliases-for-foreign-key): self-found gap via repo-audit — `FactoryBot.aliases_for(:test_id)` returned a spurious `:test_id_id` alias because the default catch-all alias rule `[/(.*)/, '\1_id']` re-appended `_id` to foreign keys. Fixed the rule to skip already-`_id`-suffixed names (`[/(.+)(?<!_id)\z/, '\1_id']`) + regression test. No maintainer-engaged unclaimed open issue survived (open bugs are AR-inherent #1736, user-error #1724/#1787, design-question #1679; GFIs #1825/#1826 claimed/merged). Verifier green: rake all_specs (441 rspec + 4 cucumber), standard clean on changed files. Lesson: the `foo` vs `foo_id` alias area is deliberately tuned (issue #1142, merged PR #1709) — keep the fix to removing the double-suffix only, never rework alias resolution.

## Mined gaps (discovered, not yet attempted)
- none yet
