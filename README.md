# site-generator-speed-01-entry

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/AhmadTurki182/site-generator-speed-01-entry/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/AhmadTurki182/site-generator-speed-01-entry/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's own makefun-site 1.0.0: it returns exactly the
same output tree for every site, in about half the CPU time.

`main.ts` is the harness driver (reads `/input/cases.json`, writes
`/output/answers.json`). `solve.js` is the whole generator, written fresh for
speed: a batched Markdown inline renderer, indexOf-based closer search with a
backslash-parity check, an ASCII fast path plus memoisation for slugs, indexOf
front-matter scanning, allocation-free word counting, and array-joined template
rendering. Nothing is cached from one case to the next.

## Run it

```sh
MAKEFUN_INPUT_DIR=<cases dir> MAKEFUN_OUTPUT_DIR=out node main.ts
```

## Verify it

On the kit's practice set the output is byte-identical to makefun-site 1.0.0 on
all 3 cases (and on 9 further cases drawn fresh from the kit's generator with
three other seeds). Median CPU over 10 runs of the whole program: 718 ms
against the house baseline's 1,354 ms — about 1.9x end to end, 2.3x on the
build alone (461 ms vs 1,062 ms).
