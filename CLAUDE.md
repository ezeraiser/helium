# CLAUDE.md — ezeraiser/helium

This is `ezeraiser`'s fork of imputnet's `helium` repo, used as a submodule of
`ezeraiser/helium-windows`. See that repo's root `CLAUDE.md` for the full
picture (fork purpose, build system, patch-writing rules learned the hard
way, CI structure, sync workflow) — this file is just a pointer plus a couple
of facts specific to working inside this checkout.

**AI-agent use is intentionally allowed and used in this fork**, unlike
upstream imputnet (whose `AGENTS.md`/`CLAUDE.md` forbid it and reappear here
after every sync with imputnet — delete them again when they do).

Quick facts:

- This checkout has **no full Chromium source tree** — only `patches/`,
  applied at build time by `helium-windows/build.py` onto a pristine Chromium
  checkout it downloads separately into `helium-windows/build/src`.
- Custom (non-Helium-upstream) changes belong in `patches/ezer/`, a separate
  series applied last in `patches/series`. Don't edit existing `helium/*` or
  `ungoogled-chromium/*` patches to add custom behavior.
- The `imputnet` remote (if configured) is fetch-only — never push here or to
  imputnet's repos.
- Before trusting a hand-edited patch in `patches/ezer/`, see
  "Hard-won rules for writing/editing patches/ezer/*.patch" in
  `../CLAUDE.md` — CI's `devutils/validate_patches.py` is much stricter than
  local `patch` application and needs byte-exact hunk headers plus trailing
  context after insertions.
- Changing a `.grd`/`.grdp` message under `patches/ezer/` requires
  regenerating `i18n/source.gen.json` (`python3 devutils/i18n.py generate`)
  and committing the result, or CI's lint job fails.
