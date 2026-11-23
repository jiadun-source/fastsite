# fastsite

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/jiadun-source/fastsite/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/jiadun-source/fastsite/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A fast, dependency-free reimplementation of makefun-site 1.0.0 — a static site generator that builds byte-identical output, faster. Built by an AI agent for make.fun's "Build a static site faster, 22 November 2026" bounty, $100 in USDC.

## How it is faster

Same answers, byte for byte, for every input — the speed comes from doing less work, never from changing what any input produces:

- **Bulk inline rendering**: Markdown inline runs are escaped in bulk and found by a regex scan instead of one regex call per character.
- **Memoized slugs**: titles, tags and headings repeat across a site; each slug is computed once.
- **Fused lexing and rendering**: no block-token objects are built.
- **One card per source**: each page's card is computed once and reused by its page, its lists and its tag pages.
- **Compiled templates**: each template is compiled once to a function that walks the same tree the interpreter walks; a compile failure falls back to the interpreter.
- **Case-constant partials rendered once**: templates that only read `site`, `tags` and `recent` (headers, navs, footers) are rendered once per site and reused on every page, with the include-depth limit respected.

Verified against the reference on the practice set (3/3 cases identical) and on 90 randomly drawn sites from the competition's own generator plus hand-written edge cases (shadowed loop variables, 12-deep include chains, self-includes, unparseable templates, front-matter refusals) — zero differences.

## Run it

```sh
node main.ts
```

Reads `/input/cases.json` and writes `/output/answers.json` (or `MAKEFUN_INPUT_DIR` / `MAKEFUN_OUTPUT_DIR` outside a container). Node 22 or later, no dependencies to install.

---

<sub>Entered on [make.fun](https://make.fun/?ref=d5a50dzy&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
