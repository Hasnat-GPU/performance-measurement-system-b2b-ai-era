# Contributing

Thanks for taking the time. This repository holds a **design document**, not a codebase, so contributing looks a little different from a typical open-source project.

The design's own §14 says it should be measured, not believed. Contributions that test it are the most valuable kind.

## Four kinds of contribution

| Kind | What it looks like | Start with |
|---|---|---|
| **Correction** | A fact, figure, citation or company practice is wrong or out of date | [Correction issue](../../issues/new?template=correction.yml) |
| **Challenge** | A premise, inference or design decision doesn't hold | [Challenge issue](../../issues/new?template=challenge.yml) |
| **Evidence** | Research or field data that supports or undermines a claim | Challenge issue, with the citation |
| **Editorial** | Typos, formatting, broken links, clearer phrasing | Pull request directly |

**Editorial fixes can go straight to a PR.** Everything else is better as an issue first — a challenge is usually a conversation, and it's a waste of your time to write a patch before we agree on the direction.

## What makes a good challenge

The document tries to state its reasoning explicitly so it can be argued with. A challenge lands best when it names:

1. **The specific claim** — quote it, with the section number.
2. **Why it fails** — a logical gap, contrary evidence, or a case where the mechanism produces a bad outcome.
3. **What you'd put in its place** — optional, but it moves the conversation forward.

Challenges that engage the reasoning are welcome regardless of tone of disagreement. "This is how it's always been done" is explicitly not an argument here, and neither is "no company does this" — the design rejects several practices that every surveyed company uses, and says why.

## Standards for evidence

The document distinguishes between kinds of claim, and contributions should too:

- **Empirical claims** (a variance figure, an attrition rate, a company's stated policy) need a source. Primary or reputable secondary.
- **Design decisions** (four bands rather than five) are arguments from stated principles. Challenge the principle or the inference, not the absence of a citation.
- **Reported company practice** changes fast. If §3 describes something a company no longer does, that's a correction — please date your source.

## Pull requests

1. Fork, then branch from `main` (`fix/broken-hbr-link`, `docs/clarify-attribution-gate`).
2. Keep changes focused. One correction per PR is easier to review than six.
3. Run the checks locally if you can:

   ```bash
   npx markdownlint-cli2 "**/*.md" "#node_modules"
   ```

4. Update [`CHANGELOG.md`](CHANGELOG.md) under `## [Unreleased]` for anything beyond a typo.
5. Fill in the PR template — the "what changed and why" field is the one reviewers actually read.

CI runs markdownlint on every push and PR. The link checker runs weekly rather than per-PR, because external link rot isn't a reason to block your contribution.

## Style

- **Prose, not bullets, for reasoning.** The document argues; bullet lists flatten arguments into assertions. Lists are for enumerable things.
- **Claims carry their derivation.** If you add a principle, say what it follows from.
- **Name the limitation.** The design's credibility rests on §14 being honest. If your addition has a failure mode, write it down.
- Sentence case for headings, Oxford comma, en dashes for ranges.

## Licensing of contributions

By contributing you agree that your contribution is licensed under [CC BY 4.0](LICENSE), the same terms as the rest of the repository.

## Conduct

This project follows the [Contributor Covenant](CODE_OF_CONDUCT.md). Disagreement is expected and welcome; contempt is not.
