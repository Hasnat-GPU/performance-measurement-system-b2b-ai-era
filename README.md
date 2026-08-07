# The Performance Measurement System for B2B Software Companies in the AI-Era

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-1f6f6b.svg)](LICENSE)
[![Quality](https://github.com/Hasnat-GPU/performance-measurement-system-b2b-ai-era/actions/workflows/quality.yml/badge.svg)](https://github.com/Hasnat-GPU/performance-measurement-system-b2b-ai-era/actions/workflows/quality.yml)
[![Links](https://github.com/Hasnat-GPU/performance-measurement-system-b2b-ai-era/actions/workflows/links.yml/badge.svg)](https://github.com/Hasnat-GPU/performance-measurement-system-b2b-ai-era/actions/workflows/links.yml)
[![Status: v1.0](https://img.shields.io/badge/status-v1.0%20design-6e7773.svg)](CHANGELOG.md)

A performance measurement system designed from first principles — for an organization where value is produced by teams, and the instrument measuring it is mostly noise.

**→ [Read it as a designed page](https://claude.ai/code/artifact/93c47a12-b0ed-49b9-800c-8279f1bdc5f3)** — typeset, with diagrams, light and dark themes

**→ [Read the source document](PERFORMANCE-MEASUREMENT-SYSTEM.md)** — the same content in Markdown, renders here on GitHub

---

## Why this exists

Most corporate performance systems are assembled from convention. This one is derived from two facts that convention ignores.

### 1. One instrument cannot do the job

A performance system has four irreducible purposes, and their information requirements **contradict each other**:

| | Learning needs | Allocation needs |
|---|---|---|
| Stakes | Near zero | High |
| Candor | Maximum | Impression-managed |
| Comparison between people | Harmful | Essential |
| Granularity | Rich and messy | Coarse and comparable |

Forcing both through one annual form is why the development half of every review is theater. This design runs **four decoupled layers** instead — and the learning instrument is structurally incapable of setting anyone's pay.

### 2. The standard instrument is mostly noise

Scullen, Mount and Goff (2000) decomposed the variance in multi-rater performance ratings:

```text
Rater's own idiosyncratic tendencies  ████████████████████████████  62%
Ratee's actual performance            █████████                     21%
Dimension and error                   ███████                       17%
```

The majority of a performance rating is about the person giving it. Organizations run firing decisions off this instrument while reporting no error bars at all. This design treats rating as what it is — a low-precision instrument — and corrects for it: rater standardization, multiple readings, published confidence ratings, and coupling only to decisions coarse enough to survive the noise.

---

## What's in the design

| § | Section | |
|---|---|---|
| 0 | The organization it's designed for | ~450 people, ~55 teams, B2B software |
| 1–2 | The framing and the measurement problem | Why one instrument fails; rater variance; Goodhart; unit-of-analysis error |
| 3 | **Field survey** | Google, Amazon, Netflix, Apple, Meta, Microsoft, Deloitte/Adobe — strengths, weaknesses, and an explicit adopt/reject decision for each |
| 4–5 | Design principles and architecture | 13 derived principles; the four-layer system |
| 6 | **Q1 — Team assessment method** | Five team dimensions, three individual axes, rater correction, confidence bands |
| 7 | **Q2 — Strategic elevation plan** | Ambiguity-based ladder, Capability Map, Talent Export Credit, succession |
| 8 | **Q3 — Recognition and reward** | Four separate currencies; no individual performance bonus |
| 9 | Twelve differentiators | The features not found in any surveyed system |
| 10–14 | Failure modes, refusals, cost, roadmap, limitations | Including stated kill criteria |

## The three questions it answers

1. **What is the comprehensive team assessment method?** Teams on five dimensions (Outcome, Reliability, Leverage, Health, Learning Rate), never ranked against each other because team difficulty isn't comparable. Individuals on three axes with statistical rater-bias correction and an explicit confidence rating — where a low-confidence negative assessment cannot trigger consequences.
2. **What is the strategic elevation plan?** A ladder defined by ambiguity absorbed rather than years served; promotion requires two cycles across **two distinct contexts**, because a single manager's opinion is one reading from one instrument. Plus organizational capability elevation, which nearly every system omits.
3. **What is the recognition and reward system?** Four deliberately separate currencies — money (slow, market-anchored, decoupled from ratings), recognition (fast, peer-driven, **non-convertible to cash**), opportunity (measured and audited), and indivisible team rewards.

## Three ideas worth stealing

- **The System Attribution Gate** — before anyone is rated down, the assessor must answer in writing whether the environment would have produced the same result for a strong performer. If two or more factors come back red, the finding lands on the organization instead.
- **The Re-recruitment Review** — Netflix's Keeper Test, inverted. Same information, but honest assessment costs the *organization money* rather than costing the *employee their job*, which flips every manager's standing incentive from downgrade to retain.
- **Layer 4** — the system publishes its own predictive validity annually, with stated kill criteria. A performance system that cannot be shown to be wrong is a ritual.

---

## Reading it

Two versions, same content:

- **[The designed page](https://claude.ai/code/artifact/93c47a12-b0ed-49b9-800c-8279f1bdc5f3)** — typeset for reading, with the variance decomposition and the four-layer architecture drawn rather than described. Adapts to light and dark themes, and prints cleanly.
- **[The Markdown source](PERFORMANCE-MEASUREMENT-SYSTEM.md)** — self-contained, renders on GitHub, diffable and quotable. This is the canonical copy.

It is long by design — a system this consequential deserves its reasoning shown rather than asserted.

If you want the short version, read **§1** (why one instrument fails), **§2.1** (the variance table), and **§9** (the differentiators). That is roughly 15 minutes and carries the argument.

## Status and intent

This is **v1.0 — a design, not a result.** The components draw on published evidence, but the *combination* has not been deployed or tested. §13 specifies a pilot with a control group and §14 states where the design is weak, both deliberately. It should be measured, not believed.

Disagreement is the point. If a premise is wrong, [open an issue](../../issues/new/choose) — the repository has a template for exactly that.

## Citing

A [`CITATION.cff`](CITATION.cff) is included, so GitHub's **"Cite this repository"** button produces a correct reference.

## License

[Creative Commons Attribution 4.0 International](LICENSE) (CC BY 4.0) — share and adapt freely, including commercially, with attribution.

Chosen over a software license deliberately: this is written work, and CC BY is the license family built for it.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Corrections, counter-evidence and challenges to the reasoning are all welcome, and are handled differently — the guide explains how.
