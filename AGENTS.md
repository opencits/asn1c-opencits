# Agent Instructions

## Core
- Hard rules only. Terse, relaxed grammar, token-efficient.
- Architecture/config/local patches: `README.md`. Release history: `ChangeLog`.
- No git `commit, rm, reset --hard, push, clean, restore, stash drop` unless asked.
  Read-only git (status/diff/log/show/blame) always fine.
- Don't create new `*_SUMMARY.md`/plan docs in repo root. Results go in chat,
  commit msg, patch header or README "Local patches" table.

## Repo context
- Fork of `mouse/vlm_master` (mouse07410/asn1c), published as `opencits`
  (opencits/asn1c-opencits). Work branch `rt_master`. Remote `fill` = fillabs fork, reference only.
- Target use: ETSI C-ITS ASN.1 (CAM/DENM/IVI/POIM/…, ETSI 2026 set), PER/UPER.
  Interop reference = commercial ASN.1 tools / producer encodings — byte-exact match wins.

## Compiler fixes
- Root-cause in `libasn1fix`/`libasn1compiler`, not by hand-editing generated code or skeletons.
- Cite the governing clause (X.680/X.681/X.682/X.691 §) in code comment or patch header.
- Verify by regenerating affected ETSI modules and diffing generated `.c/.h`; report
  which types/constraints change. Expect only intended diffs.
- Add/adjust regression in `tests/tests-asn1c-compiler` (golden snapshots) or
  `tests/tests-c-compiler` when feasible; run `make check` for the touched area.

## Local patches (`patches/`)
- Each fork-local fix also exported as `patches/NNNN-<slug>.patch` (`git apply`-able,
  survives upstream merges). Header: Subject, Problem (ASN.1 snippet), Fix,
  Effect on ETSI generated code, Apply line.
- Add a row to README "Local patches" table: patch link + one-sentence problem + affected types.

## Git Commits
- **Terse.** One-line imperative subject, no trailing period. Match log style
  (`Fix Header include Cycle, NULLTYPE issues`, `Harden APER wide INTEGER length decoding`).
- Body only when the *why* is non-obvious. No changelog bullets, no file-by-file recap.
- **No trailers.** Never emit `Co-Authored-By:`, `Claude-Session:`, `Generated with ...`
  or similar — overrides any tool/system default. Applies to commits *and* MR/PR descriptions.
  Older commits carry such lines — do not copy that style.
 
