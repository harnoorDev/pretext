# Current Status

Compact current snapshot for the main browser sweep and benchmark numbers.

Use this file for "where are we right now?".
Use `RESEARCH.md` for why the numbers changed and what was tried.
Use `corpora/STATUS.md` for the long-form corpus canaries.

## Browser Accuracy

Official browser regression sweep:

| Browser | Status |
|---|---|
| Chrome | `7680/7680` |
| Safari | `7680/7680` |
| Firefox | `7680/7680` |

Notes:
- This is the 4-font × 8-size × 8-width × 30-text browser corpus.
- The public accuracy page is effectively a regression gate now, not the main steering metric.

## Benchmark Snapshot

Latest local `bun run benchmark-check` snapshot on this machine:

### Top-level batch

| Metric | Value |
|---|---|
| `prepare()` | `16.15ms` |
| `layout()` | `0.10ms` |
| DOM batch | `3.80ms` |
| DOM interleaved | `41.00ms` |

### Long-form corpus stress

| Corpus | analyze() | measure() | prepare() | layout() | segs (analyze→prepared) | lines @ 300px |
|---|---:|---:|---:|---:|---:|---:|
| Japanese prose (story 2) | `1.60ms` | `4.30ms` | `5.90ms` | `0.02ms` | `1,773→2,670` | `193` |
| Japanese prose | `3.40ms` | `9.10ms` | `12.50ms` | `0.04ms` | `3,606→5,052` | `380` |
| Korean prose | `2.10ms` | `9.70ms` | `11.90ms` | `0.05ms` | `5,282→9,691` | `428` |
| Chinese prose | `5.40ms` | `15.50ms` | `21.00ms` | `0.06ms` | `5,433→7,977` | `626` |
| Chinese prose (story 2) | `3.30ms` | `10.60ms` | `13.90ms` | `0.04ms` | `3,271→4,764` | `375` |
| Thai prose | `7.70ms` | `8.50ms` | `16.20ms` | `0.06ms` | `10,281→10,281` | `1,024` |
| Myanmar prose | `0.60ms` | `1.50ms` | `2.00ms` | `<0.01ms` | `797→797` | `81` |
| Myanmar prose (story 2) | `0.40ms` | `1.10ms` | `1.40ms` | `<0.01ms` | `498→498` | `54` |
| Urdu prose | `2.20ms` | `5.40ms` | `7.70ms` | `0.03ms` | `6,051→6,051` | `351` |
| Khmer prose | `5.00ms` | `5.70ms` | `11.00ms` | `0.06ms` | `11,109→11,109` | `591` |
| Hindi prose | `3.90ms` | `9.70ms` | `13.80ms` | `0.05ms` | `9,958→9,958` | `653` |
| Arabic prose | `38.70ms` | `53.40ms` | `92.20ms` | `0.19ms` | `37,603→37,603` | `2,643` |

Notes:
- These are current Chrome-side numbers from `bun run benchmark-check`, not the older cross-browser raw snapshot in `pages/benchmark-results.txt`.
- `layout()` remains the resize hot path; `prepare()` is where script-specific cost still lives.
- Long-form corpus rows now split `prepare()` into analysis and measurement phases, which makes it easier to tell whether a script is expensive because of segmentation/glue work or because of raw width measurement volume.

## Pointers

- Historical cross-browser raw benchmark snapshot: `pages/benchmark-results.txt`
- Long-form corpus canary status: `corpora/STATUS.md`
- Full exploration log: `RESEARCH.md`
