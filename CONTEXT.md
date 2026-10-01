# thoughtbot/factory_bot context
> refreshed 2026-10-01 | upstream default: main @ 18ae8b5 (unchanged)

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

- 2026-09-25 engine/loop (ANY repo) — PR #4 opened (fix/no-op-error-assertions): self-found test-quality gap via repo-audit — the "it fails with an unknown sequence or factory name" spec nested `.to raise_error` INSIDE the `expect {}` block, so the matcher never ran: a no-op false-green (any message "passed"). Fixed to `expect { generate(...) }.to raise_error KeyError, /Sequence not registered: .../` and corrected the old regexes (real messages are `test`, `user/test`, `admin/counter` — the old lines asserted `:test`, `user:test`, `"admin:counter"` which never matched the actual `KeyError` texts). Proven on live upstream via a standalone script that still "passes" under the old nested form with a deliberately-wrong message, and fails with the matcher outside the block. Verifier green: rake all_specs (unit + 441 rspec + 4 cucumber), standard clean on the changed spec.

- 2026-10-01 trivial/minor-fix pass (loop-trivial) — PR #5 opened (fix/docs-comment-typos): 6 genuine one-word fixes across 5 files, deliberately disjoint from OPEN PR #2's file set (PR #2 = .github/REPRODUCTION_SCRIPT.rb, GETTING_STARTED.md, SECURITY.md, docs/src/activesupport-instrumentation/summary.md, docs/src/callbacks/*.md, docs/src/ref/register_strategy.md, docs/src/ref/sequence.md, docs/src/sequences/generating.md, docs/src/sequences/rewinding.md — none touched here). Fixes: lib/factory_bot/syntax/methods.rb `:my_trair`->`:my_trait` (2 doc-example lines; uri_manager.rb already had `:my_trait`), lib/factory_bot/uri_manager.rb comment `sripping`->`stripping`, lib/factory_bot/sequence.rb comment `auto-recues`->`auto-rescues`, spec/acceptance/attribute_aliases_spec.rb comment `asignes`->`assigns`, docs/src/ref/method_missing.md `as a argument`->`as an argument`. Exhaustive search (codespell 2.4.3 + pyspellchecker over all tracked .md/.rb prose, whole-repo dead-link sweep of 97 URLs, article/double-word greps) surfaced NO other genuine misspelling. English variants respected (repo is US English; no dialect normalisation). Dead links left UNFIXED (no meaning-preserving replacement): README.md:23 + GETTING_STARTED.md:10 `upcase.com/videos/factory-bot` (404; upcase folds into thoughtbot.com/resources, no equivalent video), RELEASING.md:42 `thoughtbot/handbook/.../rubygems.md#managing-rubygems` (404; thoughtbot/handbook repo deleted, no live thoughtbot replacement and the thoughtbot/guides ruby/how-to/release_a_ruby_gem.md does NOT cover gem ownership, so changing URL would change meaning), RELEASING.md:28 `compare/vLAST_VERSION...main` (placeholder, not a link bug). NO Ruby toolchain in this container (no ruby/gem/bundle, no sudo/apt) so the suite could not be run locally; all 6 changes are inside `#` comments or one markdown prose line, and `git diff --check` is clean. Fork registers 0 workflows (known fork artifact), so no fork CI run.

## Mined gaps (discovered, not yet attempted)
- 2026-09-25 no-op error assertions in `spec/acceptance/sequence_spec.rb` (unknown-sequence spec) — now DONE as PR #4. 
- (future) consider scanning other `expect { ... .to raise_error ... }` nests across the acceptance specs — the same no-op pattern may exist elsewhere; dedupe before touching.
