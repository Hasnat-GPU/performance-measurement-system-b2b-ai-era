# The Meridian Performance System

**A performance measurement system designed from first principles**

Version 1.0 · Design document · August 2026

---

## Table of contents

- [0. The organization this is designed for](#0-the-organization-this-is-designed-for)
- [1. What a performance system is actually for (and why one instrument cannot do it)](#1-what-a-performance-system-is-actually-for)
- [2. The measurement problem nobody designs around](#2-the-measurement-problem-nobody-designs-around)
- [3. Field survey: what the big companies do, and what survives contact with evidence](#3-field-survey)
- [4. Design principles](#4-design-principles)
- [5. System architecture: four decoupled layers](#5-system-architecture)
- [6. **Question 1 — The comprehensive team assessment method**](#6-question-1)
- [7. **Question 2 — The strategic elevation plan**](#7-question-2)
- [8. **Question 3 — The recognition and reward system**](#8-question-3)
- [9. Added features: the twelve differentiators](#9-added-features)
- [10. Failure modes and the defenses against them](#10-failure-modes)
- [11. What this system refuses to do](#11-what-this-system-refuses-to-do)
- [12. Cost model and scaling](#12-cost-model-and-scaling)
- [13. Implementation roadmap, with kill criteria](#13-implementation-roadmap)
- [14. Honest limitations](#14-honest-limitations)
- [Sources](#sources)

---

<a name="0-the-organization-this-is-designed-for"></a>

## 0. The organization this is designed for

No design is portable without knowing its load. I am designing for a specific organization, and stating it plainly so every decision below can be checked against it.

**Meridian** — a B2B software company.

| Parameter | Value |
|---|---|
| Headcount | ~450 |
| Teams | ~55, average size 6–9 |
| Functions | Engineering, Product, Design, Data, Revenue, Customer Operations, G&A |
| Geography | 4 time zones, hybrid, no single dominant office |
| Management depth | 4 layers (IC → Team Lead → Director → Exec) |
| Work character | Long-horizon, high-interdependence, high-variance outcomes, hard to attribute individually |
| Talent market | Competitive; senior specialists are scarce and expensive to replace |
| Growth stage | Past product-market fit, scaling; margin discipline matters |

Two properties of this organization drive nearly every decision that follows:

1. **Outcomes are produced by teams and systems, not by individuals acting alone.** A single engineer's quarter can look excellent or terrible depending on the dependency they were handed. Any system that measures individuals against outcomes they do not control is measuring luck.
2. **The organization is too small to absorb the cost of a heavy process, and too large to run on the founder's memory.** At 450 people no one can hold the whole talent picture in their head, but a Google-scale calibration apparatus would consume a meaningful fraction of total capacity.

Scaling notes for 50 / 500 / 5,000 people appear in [§12](#12-cost-model-and-scaling).

---

<a name="1-what-a-performance-system-is-actually-for"></a>

## 1. What a performance system is actually for (and why one instrument cannot do it)

Start by refusing the usual framing. A performance system is not "a way to evaluate people." That is a description of a mechanism, not a purpose. Purposes are these four, and they are irreducible — an organization needs all of them:

| # | Job | The question it answers |
|---|---|---|
| **J1** | **Direct attention** | What matters here? Where should effort go? |
| **J2** | **Generate learning signal** | How do people and teams get better at the work? |
| **J3** | **Allocate scarce goods** | Who gets money, promotion, headcount, and the interesting problems? |
| **J4** | **Protect the organization** | Where is failure accumulating? Are decisions fair and defensible? |

Here is the observation the entire design rests on: **these four jobs have contradictory information requirements.** They are not merely different. They actively poison each other when forced through one instrument.

| Requirement | J1 Attention | J2 Learning | J3 Allocation | J4 Protection |
|---|---|---|---|---|
| **Stakes for the person** | Low | **Must be near zero** | **Must be high** | High |
| **Candor needed** | Moderate | **Maximum** | Moderate (people manage impressions) | High |
| **Frequency** | Continuous | **Continuous** | **Periodic and predictable** | Event-driven |
| **Granularity** | Few, stable signals | Rich, specific, messy | **Coarse and comparable** | Thresholded |
| **Comparability across people** | Irrelevant | **Harmful** | **Essential** | Essential |
| **Written record** | Light | Disposable | **Durable** | **Durable and defensible** |

Read the conflicts. Learning requires the lowest possible stakes, because a person will not tell you what they are bad at if the answer determines their bonus. Allocation requires the highest possible stakes, because a decision with no consequence is not an allocation. Learning requires messy specificity; allocation requires clean comparability. Learning must not compare people; allocation must.

**Nearly every failed corporate performance system fails here, at the root.** The annual review is asked to be a development conversation, a compensation input, a promotion gate, and a legal artifact, in one meeting, on one form, with one number. The result is predictable: the person being reviewed correctly perceives the stakes and stops disclosing weakness, the manager correctly perceives that the form determines money and inflates or deflates accordingly, and the "development" portion becomes theater performed by two people who both know what the meeting is really about.

> **Design Decision 1 — Separation.** Meridian runs four instruments, not one. They have different clocks, different stakes, different audiences, and different data. The learning instrument is structurally incapable of setting anyone's pay. This is not a nicety; it is the load-bearing wall.

---

<a name="2-the-measurement-problem-nobody-designs-around"></a>

## 2. The measurement problem nobody designs around

Before designing an instrument, it is worth asking how good the standard instrument is. The answer is bracing.

### 2.1 Most of a performance rating is about the rater

Scullen, Mount and Goff (2000, *Journal of Applied Psychology*) decomposed the variance in multi-rater performance ratings across two large datasets (n = 2,350 and n = 2,142 managers, each rated on three dimensions by seven raters). The finding:

| Source of variance in a performance rating | Dataset 1 | Dataset 2 |
|---|---|---|
| **The rater's idiosyncratic tendencies** | **62%** | **53%** |
| The ratee's actual performance | 21% | 25% |
| Everything else (dimension, error) | 17% | 22% |

Rater variance exceeded ratee variance by 1.21× for supervisors, 2.08× for peers and 1.86× for subordinates. Deloitte found the same thing in its own data and said so publicly: ratings "revealed more about team leaders than about the people they were rating."

Sit with the implication. When a manager rates someone a 3 instead of a 4, the single most likely explanation is not that the person performed at a 3. It is that this manager is a person who gives 3s. We are running high-stakes decisions — pay, promotion, termination — off an instrument in which the majority of the signal is noise from the measuring device.

This does not mean rating is worthless. It means **rating is a low-precision instrument, and low-precision instruments must be used the way low-precision instruments are used**: with error correction, with multiple independent measurements, with wide confidence intervals, and coupled only to decisions coarse enough to survive the noise. You can weigh a truck on a bathroom scale if all you need to know is "more than a ton." You cannot use it to price gold.

### 2.2 The measure that becomes a target stops measuring

Goodhart's law, in Marilyn Strathern's now-standard paraphrase: *when a measure becomes a target, it ceases to be a good measure.* Campbell's law says the same thing with more menace: the more a quantitative indicator is used for social decision-making, the more it will distort and corrupt the process it was meant to monitor.

This is not a caveat to bolt on at the end. It is a *thermodynamic property of measurement under stakes*. Any metric attached to consequence will decay, and the decay rate is proportional to the stakes and inversely proportional to how hard the metric is to game. Ticket counts produce ticket-splitting. Lines of code produce verbosity. Incident-response speed produces under-classification of incidents. Customer satisfaction scores produce the begging-for-a-10 ritual that has made every such score globally uninformative.

The conventional response is to search for an ungameable metric. There isn't one. The correct response is to **design for decay**: pair every metric with a guardrail it may not degrade, give every metric an expiry date, red-team the metric set adversarially before shipping it, and keep a portion of the sensing layer permanently disconnected from stakes so that at least some of your instruments stay honest.

### 2.3 The unit of measurement is usually wrong

W. Edwards Deming argued that the overwhelming majority of variation in output — he put it at 94% — belongs to the system, not to the individual working within it. The precise figure is rhetorical rather than measured, but the direction is not in dispute, and modern evidence points the same way. Google's Project Aristotle studied 180 teams across 250 attributes and found that *who is on the team* mattered less than *how the team works together*, with psychological safety the strongest differentiator of high-performing teams. Deloitte's own team research found the three items most predictive of team performance were about the team environment, not individual traits.

If most variation is systemic and most value is produced by teams, then an organization that measures only individuals is measuring the least explanatory variable it has access to. Meridian therefore measures the **team** against outcomes and the **individual** against contribution and trajectory — never the individual against an outcome they do not control.

### 2.4 Outcomes are a biased sample of decisions

In high-variance work, good decisions routinely produce bad outcomes and bad decisions routinely produce good ones. Judging exclusively on outcomes — what poker players call *resulting* — systematically rewards people who took unwise risks that happened to pay and punishes people who made correct calls in bad conditions. Over a few cycles this teaches the organization to be reckless in bull markets and timid in bear ones.

So Meridian evaluates **decisions on the quality of the process and the information available at the time**, and **outcomes on results**, and keeps the two conclusions separate rather than collapsing them into one judgment.

---

<a name="3-field-survey"></a>

## 3. Field survey: what the big companies do, and what survives contact with evidence

For each system: the mechanism, what it is genuinely good at, where it breaks, and the explicit transfer decision for Meridian.

### 3.1 Google — OKRs + GRAD

**Mechanism.** Objectives and Key Results for goal-setting, nominally decoupled from evaluation. GRAD (Googler Reviews and Development) rates impact on a five-tier scale from *Not Enough Impact* to *Transformative Impact*, semi-annually, with continuous check-ins and committee calibration. Promotion runs as a separate, evidence-heavy packet process. Ratings drive bonus and equity multipliers.

Google announced changes taking effect in the 2026 compensation cycle: managers may award the coveted *Outstanding Impact* rating to more people, funded — explicitly, "budget-neutral" — by lowering the multipliers for the *Significant* and *Moderate Impact* middle tiers. Reported knock-on effects: the share of employees landing in the lowest category rises from roughly 2% to as much as 6%, while the share in the top two tiers falls from about 27% to about 22%.

**Strengths.**

- OKRs, used properly, separate ambitious goal-setting from evaluation. Setting a target you expect to miss is only rational if missing it is not punished.
- Genuine investment in evidence-based management: Project Oxygen (what makes managers effective) and Project Aristotle (what makes teams effective) are real research, and Aristotle's psychological-safety finding is one of the most useful results in the field.
- Calibration committees do reduce single-manager idiosyncrasy — the exact error identified in §2.1.
- "Impact" as the unit of assessment is better than effort, hours, or output volume.

**Weaknesses.**

- **The rating distribution is set by the compensation budget.** The 2026 change is the tell: the tiers were re-cut and the multipliers re-weighted to keep total spend flat. That means the tier is not a measurement of the person; it is a share of a fixed pool wearing measurement's clothes. Two people doing identical work in different years receive different labels because the budget changed. Once employees work this out — and they do — the rating loses its power to inform, while keeping all of its power to demoralize.
- The separate promotion packet creates a well-documented distortion: people select work for its *legibility to a promotion committee* rather than its value to the company. Unglamorous, critical work — maintenance, enablement, reliability — becomes career-negative.
- Committee calibration adds a political layer in which an employee's outcome depends materially on whether their manager argues well in a room the employee cannot enter.

**Transfer decision.** **Adopt** calibration, the impact framing, and the commitment to studying your own management empirically. **Reject** budget-derived distributions. → *Design rule: the budget constrains the payout, never the rating.* **Reject** the standalone promotion packet; Meridian's evidence ledger replaces it ([§7.1](#7-question-2)).

### 3.2 Amazon — Leadership Principles + Forte + OLR + URA

**Mechanism.** Sixteen Leadership Principles as a shared behavioral vocabulary. Forte as the feedback tool. Organization and Leadership Review (OLR) talent calibration twice yearly, roughly Q1 and Q3. A corporate **Unregretted Attrition** target — the percentage of employees the company would like to see leave, voluntarily or otherwise — reported at around 6%. Underperformers enter **Focus** (a coaching plan of one to three months) and, on failing it, **Pivot**: choose severance or an improvement plan with hard deadlines.

**Strengths.**

- The Leadership Principles are the single most underrated mechanism in this survey. A shared, concrete, memorized behavioral vocabulary directly attacks the rater-variance problem from §2.1: when every rater is describing the same named constructs with the same examples, their idiosyncratic mental models converge. This is real measurement engineering, whether or not Amazon frames it that way.
- The writing culture (six-pagers, narrative memos) produces durable, timestamped evidence of thinking as a byproduct of doing the work — the cheapest performance data there is.
- "Unregretted" is a genuinely useful mental frame *as a question*: would we be sorry if this person left?

**Weaknesses.**

- **URA is a quota on human outcomes, and a quota inverts measurement.** The target — 6% must go — exists before any data is collected. That is Campbell's law implemented as policy. Documents obtained by the *Seattle Times* describe software-supported processes for hitting turnover targets among low-ranked office staff that closely resemble stack ranking, despite the company's denials.
- The predictable second-order effect of a quota is defensive hiring: managers described as hiring people they intend to sacrifice to the number. Any system that makes it rational to hire someone in order to fire them has a defect no amount of tuning fixes.
- A standing exit quota is the direct antagonist of psychological safety, which Aristotle identifies as the strongest predictor of team performance. The organization is spending on one hand what it takes with the other.

**Transfer decision.** **Adopt** the shared behavioral vocabulary (Meridian's Operating Principles) and writing-as-evidence. **Reject absolutely** any target on the distribution of human outcomes. → *Design rule: no quota, ceiling, or floor may be set on how many people land in any performance band.*

### 3.3 Netflix — Keeper Test + context-not-control + top-of-market cash

**Mechanism.** No formal performance reviews; the CTO has stated so publicly. An annual 360 as a safety net, framed explicitly as developmental — colleagues name what to *start, stop, continue*. Continuous informal candor. The **Keeper Test**: a manager asks whether they would fight to keep this person if they resigned today; if not, the person is offered generous severance and exits. Compensation is top-of-market, all-cash, set against the person's external market value, with no bonus and no rating-driven multiplier.

**Strengths.**

- This is the purest existing implementation of the thesis in §1 and §2.1. Netflix looked at the low-precision instrument and *removed it* rather than adding decimal places, replacing it with high-frequency candor plus a single, coarse, binary decision. **Coarse decisions tolerate noisy inputs.** A bathroom scale can answer "more than a ton."
- Paying top-of-market in cash decouples compensation from the measurement cycle entirely. If money is settled and generous, the rating no longer has to carry it — which removes the main reason both parties lie during reviews. This is the most important idea in the survey and Meridian takes it.
- Severance is treated as a cost of running a demanding standard, not as a punishment. Exits are fast, funded, and unstigmatized.

**Weaknesses.**

- **The Keeper Test is an instrument of fear, and fear is expensive.** It manufactures permanent, unresolvable job insecurity by design. This suppresses exactly the behaviors psychological safety produces — dissent, admission of error, unpopular risk-taking, asking for help. Netflix pays for a highly capable workforce and then installs the one mechanism most likely to make that workforce hide its problems.
- There is **no development pathway**. You are kept or you are paid to leave. This externalizes talent development onto the labor market, which works only if you can always buy fully-formed senior people. It is structurally hostile to anyone early in career, anyone returning from leave, and anyone whose contribution is real but slow to become legible.
- It makes a single manager's idiosyncratic preferences maximally consequential, with no calibration and no appeal — the §2.1 error at maximum stakes and minimum correction.

**Transfer decision.** **Adopt** pay decoupled from ratings, personal-market-anchored compensation, high-frequency candor, coarse decisions, and generous exits. **Adapt, do not adopt, the Keeper Test.** Meridian replaces it with the **Re-recruitment Review** ([§8.1](#8-question-3)), which extracts identical information — is this person worth their market price to us? — while placing the burden of action on the organization rather than the anxiety on the employee.

### 3.4 Apple — functional organization + DRI + free-form written review

**Mechanism.** A functional organization in which leaders are domain experts rather than general managers — "experts leading experts." Every consequential piece of work has a **DRI**, a single Directly Responsible Individual. Reviews run semi-annually plus an end-of-year cycle; each employee is reviewed by three or four executives in addition to peers and direct reports, against **teamwork, innovation, and results**. Feedback is written free-form, without a numeric scale. Compensation is discretionary and equity-weighted. The whole process is opaque from outside and largely from inside.

**Strengths.**

- **Expert evaluation is the highest-leverage and least-discussed variable in performance measurement.** The accuracy ceiling of any assessment is set by whether the evaluator can recognize good work in that domain. A manager who cannot read the code, the design, or the model cannot distinguish excellent from adequate, and will fall back on proxies — confidence, visibility, hours, likeability — which is precisely how rater variance enters. Apple's structure attacks the problem at its source instead of correcting for it downstream.
- Free-form writing refuses false precision. A written paragraph cannot be averaged into a spurious 3.4, and it forces the evaluator to produce reasons rather than a number.
- DRI eliminates diffusion of responsibility — the failure mode in which a project has six contributors and no owner, and post-hoc attribution becomes impossible.
- Three axes including *teamwork* and *innovation* alongside *results* is broader than most, and specifically funds behavior that pure results-measurement destroys.

**Weaknesses.**

- **Opacity is the fatal flaw.** With no published ladder and no published criteria, employees cannot self-assess, cannot direct their own development, and cannot tell whether an outcome was earned or arbitrary. Worse, no one can audit for bias — an unpublished, discretionary, executive-judgment system is exactly the environment in which demographic disparities accumulate invisibly and undisprovably.
- It scales through the personal judgment of a small number of leaders, which travels badly and creates single points of failure.
- Secrecy blocks internal learning: teams cannot see what excellence looked like elsewhere in the company.

**Transfer decision.** **Adopt** expert evaluation as a *structural requirement* (see Design Principle 10), DRI, free-form written assessment, and the three-axis breadth. **Reject** opacity outright. → *Design rule: every criterion, every ladder level, every band definition and every aggregate distribution is published internally.*

### 3.5 Meta — Performance Summary Cycle with a mandated bottom bucket

**Mechanism.** PSC twice yearly, January and July, heavy on peer review. Ratings drive the individual bonus multiplier, equity refresh size, and salary movement directly. In January 2025 the company terminated roughly 5% of staff as low performers. For the following cycle, the mandated share of employees to be placed in the "below expectations" tier rose from 12–15% to **15–20%** for teams of 150 or more.

**Strengths.**

- Peer input at scale, which is at least a partial answer to single-rater noise.
- Unusual honesty about what the rating is *for*. Meta does not pretend the rating is developmental; it says plainly that it determines money. Given the conflicts in §1, an honest allocation instrument is better than a dishonest hybrid.

**Weaknesses.**

- A mandated bottom bucket applied to a noisy instrument does not select the weakest performers. It selects on **rater severity, team difficulty, tenure-in-team, and visibility** — because those are the variables with the most variance in the measurement, per §2.1. A person can be moved into the bottom bucket by joining a strong team.
- A six-month cycle with direct money consequences systematically punishes long-horizon work. Rational response: choose projects that finish inside the window.
- Applying the quota only to teams of 150+ reveals that it is an aggregate budgeting device, not a judgment about individuals.

**Transfer decision.** **Reject** forced distribution in all forms. **Adopt** the honesty: Meridian states in writing what each instrument is for and what it can do to you.

### 3.6 Microsoft — the reversal, and the re-tightening

**Mechanism.** Microsoft abandoned stack ranking in November 2013 after concluding it damaged collaboration and innovation, replacing it with **Connects** — flexible, continuous check-ins — and a manager standard of "model, coach, care." Impact is assessed on three dimensions: your own work, your **contribution to others' work**, and your **leverage of others' work**. Rewards run on a 0–200 scale. In 2025 the company tightened: a formalized global PIP with a Global Voluntary Separation Agreement alternative available year-round, a two-year rehire ban for anyone exiting with a low rating or during a PIP, and a bar on internal transfers for low-rated employees still at the company — after terminating roughly 2,000 people for performance without severance.

**Strengths.**

- **The 2013 reversal is the most valuable natural experiment in this entire field.** A very large company ran forced ranking for years, concluded it damaged the business, and successfully exited it. When someone proposes stack ranking, this is the evidence that the burden of proof is on them.
- The three impact dimensions are excellent and Meridian takes them nearly intact. *Contribution to others* and *leverage of others* explicitly pay people for making colleagues better — which is exactly the behavior forced ranking destroys, and exactly the behavior a team-based organization runs on.

**Weaknesses.**

- The 2025 re-tightening demonstrates the field's central political dynamic: under margin pressure, organizations regress toward punitive measurement, because it is cheap and looks decisive. Any design that does not anticipate this pressure will not survive it.
- **The internal-transfer bar is actively counterproductive.** Poor fit between a person and a role is one of the most common causes of low performance and the cheapest to fix. Blocking transfer removes the least expensive remedy and converts a solvable placement problem into an expensive termination and rehire. It optimizes the appearance of rigor over the economics of it.

**Transfer decision.** **Adopt** the three-dimension impact model and the 2013 evidence. **Invert** the transfer bar: at Meridian, sustained low assessment *triggers* a fit review in which internal transfer is a first-class, actively-supported option ([§7.4](#7-question-2)).

### 3.7 The reinvention wave — Deloitte and Adobe

**Deloitte.** Counted the cost of its own system and found it consumed close to **2 million hours per year**. Concluded that ratings revealed more about raters than ratees. Redesigned around a short instrument completed by the team leader after each project or at least quarterly, whose defining move is that it asks the leader **what they would do**, not what they think of the person — behavioral intention rather than trait judgment. It also found that the items most predictive of team performance were about the team's environment: coworkers committed to quality work, an inspiring mission, and the chance to use one's strengths daily.

**Adobe.** Killed the annual review in 2012 for **Check-in**: regular manager–employee conversations on goals, feedback and development, with no numeric ratings and no forced ranking. Results reported since: roughly **30% drop in voluntary turnover**, **80,000–100,000 manager hours recovered per year**, the February attrition spike gone — and, notably, a **~50% increase in involuntary departures**, because managers stopped deferring difficult conversations to a distant review date.

**Strengths.** The intention-question insight is the single most important methodological advance in the field, and it follows directly from §2.1: if the majority of variance is the rater, stop asking the rater to be a measuring device and start asking them to be an actor. "I would choose this person for my team again" is a claim about the rater's own future behavior, which they are qualified to make. "This person has strong analytical skills" is a claim about an unobservable trait, which they are not. Counting the hours the system consumes is the other advance — a system's cost is a design constraint, not an afterthought.

**Weaknesses.** Deloitte's answers still funnel into a rating, so the stakes eventually leak back in. And several organizations that removed ratings entirely later reinstated them, for a reason worth taking seriously: when you delete the rating you do not delete the judgment, you only make it invisible. People still get different bonuses and promotions; they just can no longer see the basis, and disparities become harder to detect and challenge. Adobe's 50% rise in involuntary exits is honest evidence that "no ratings" is not automatically gentler.

**Transfer decision.** **Adopt** intention-based rater items, per-project rather than per-calendar cadence, and an explicit hours budget. **Reject** rating abolition. → *Design rule: do not delete the rating; fix the rating and publish its error bars.*

### 3.8 Comparison at a glance

| | Google | Amazon | Netflix | Apple | Meta | Microsoft | Deloitte/Adobe |
|---|---|---|---|---|---|---|---|
| **Cadence** | 2×/yr + check-ins | 2×/yr (OLR) | Continuous + annual 360 | 2×/yr + EOY | 2×/yr | Continuous (Connects) | Per-project / continuous |
| **Rating scale** | 5 impact tiers | Tiered + LP assessment | **None formal** | Free-form written | Tiered | 0–200 impact | Removed (Adobe) |
| **Forced distribution** | Budget-shaped | **URA ~6% target** | No (Keeper Test) | Undisclosed | **15–20% bottom** | Dropped 2013, tightening 2025 | No |
| **Pay coupling** | Direct multipliers | Direct | **Decoupled** | Discretionary | Direct | Direct | Loosened |
| **Peer input** | Yes | Yes (Forte) | Yes (360) | Yes + 3–4 execs | Heavy | Yes | Reduced |
| **Team-level assessment** | Weak | Weak | Weak | Weak | Weak | Weak | **Emphasized** |
| **Best idea to steal** | Calibration; impact framing | Shared behavioral vocabulary | Pay decoupling; coarse decisions | Expert evaluators; DRI | Honesty about purpose | Contribution-to-others axis | Intention questions; cost budget |
| **Worst idea to avoid** | Budget-set distributions | Exit quotas | Fear as a mechanism | Opacity | Forced bottom bucket | Transfer bars | Rating abolition |

**The pattern across all seven.** Every one of these companies has a sophisticated apparatus for measuring individuals and almost nothing for measuring teams — despite each of them having produced or endorsed research showing that teams and systems explain most of the variance. That gap is where Meridian's design puts its weight.

---

<a name="4-design-principles"></a>

## 4. Design principles

Each principle states what it is derived from, so it can be argued with rather than merely obeyed.

**P1 — Separate the four jobs into four instruments.**
*From §1.* Development, allocation, attention-direction and protection have contradictory information requirements. One form cannot serve them. Meridian's learning instrument is structurally incapable of setting pay.

**P2 — Match instrument precision to decision granularity.**
*From §2.1.* An instrument in which half the variance is noise supports a three- or four-way decision, not a nine-way one and never a decimal. Meridian uses four individual bands and three team bands, and publishes no composite numeric score.

**P3 — No target may be set on the distribution of human outcomes.**
*From §3.2, §3.5, §3.6.* No quota, no curve, no floor, no ceiling on how many people land anywhere. The budget constrains total payout; it never constrains the assessment.

**P4 — Ask raters what they would do, not what they think.**
*From §2.1, §3.7.* Behavioral-intention items are answerable by the rater from direct knowledge. Trait items require the rater to be a measuring instrument they are not.

**P5 — Measure teams on outcomes; measure individuals on contribution and trajectory.**
*From §2.3.* Never hold an individual to an outcome they do not control. Never let a team's outcome disappear into individual scores.

**P6 — Every metric ships with a guardrail and an expiry date.**
*From §2.2.* No metric is deployed alone; each is paired with a metric it may not degrade. Every metric expires after four cycles and must be re-justified to survive.

**P7 — Accumulate evidence continuously; judge periodically.**
*From recency bias.* Review should be an act of *retrieval*, not *recall*. Unaided recall over six months is dominated by the last six weeks and by the loudest work.

**P8 — Attribute to the system before attributing to the person.**
*From §2.3.* Before any low assessment is finalized, the assessor must answer in writing whether the environment would have produced this result for a strong performer.

**P9 — Judge decisions on process, outcomes on results, and keep the conclusions separate.**
*From §2.4.* In high-variance work, collapsing the two teaches recklessness.

**P10 — Evaluators must be able to recognize good work in the domain they assess.**
*From §3.4.* This is a hiring and org-design constraint, not a training one. A team lead who cannot read the work is disqualified from assessing its quality and may assess only collaboration and reliability, with technical assessment sourced from a qualified peer.

**P11 — Publish everything except individual pay.**
*From §3.4.* Criteria, ladders, band definitions, aggregate distributions, calibration outcomes, and the system's own accuracy statistics. Unpublished systems cannot be audited, and unauditable systems accumulate bias.

**P12 — The system must be falsifiable and must measure itself.**
*From the whole field's absence of it.* A performance system with no evidence that it predicts anything is a ritual. Meridian publishes its own predictive validity annually and will scrap components that fail.

**P13 — Cap the cost.**
*From §3.7.* Measurement consumes the capacity it measures. Meridian's total measurement burden is capped at **0.9% of working hours** (≈15 hours per person per year, all-in). Any proposed addition must name what it displaces.

---

<a name="5-system-architecture"></a>

## 5. System architecture: four decoupled layers

```text
┌──────────────────────────────────────────────────────────────────────────┐
│  LAYER 1 — SENSING                          continuous · ZERO stakes     │
│  Contribution Ledger · Signal Pulses · Team Telemetry · Recognition      │
│  Job: capture evidence accurately. Never converts directly to money.     │
└───────────────────────────────┬──────────────────────────────────────────┘
                                │  evidence (visible to the subject)
                                ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  LAYER 2 — JUDGMENT                         2×/year · structured         │
│  Team Assessment (5 dimensions) · Individual Assessment (3 axes)         │
│  Error correction: rater fingerprinting · System Attribution Gate ·      │
│  confidence rating · calibration without quotas                          │
│  Output: written narrative + coarse band + confidence + flags            │
└───────────────────────────────┬──────────────────────────────────────────┘
                                │  bands, flags, narratives
                                ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  LAYER 3 — CONSEQUENCE           money: 1×/year · role: continuous       │
│  Compensation · Promotion · Role & fit decisions · Opportunity           │
│  Deliberately lagged and coarse-grained. Budget limits payout, not band. │
└───────────────────────────────┬──────────────────────────────────────────┘
                                │  outcomes over time
                                ▼
┌──────────────────────────────────────────────────────────────────────────┐
│  LAYER 4 — META                             1×/year · published          │
│  Predictive validity · rater reliability · distribution & equity audit · │
│  cost · trust survey · gaming detection · metric sunset review           │
│  Job: prove the system works, or change it.                             │
└──────────────────────────────────────────────────────────────────────────┘
```

**The decoupling is the point.** Layer 1 is safe because nothing in it converts to money without passing through human judgment in Layer 2. Layer 2 is honest because Layer 3 cannot reach back and reshape it to fit a budget. Layer 4 exists because a system that cannot be shown to be wrong cannot be improved.

---

<a name="6-question-1"></a>

## 6. Question 1 — The comprehensive team assessment method

> *"What is your comprehensive team assessment method?"*

**Short answer.** Teams are assessed twice a year on five dimensions — Outcome, Reliability, Leverage, Health and Learning Rate — using evidence accumulated continuously rather than recalled at review time. Assessment produces a written narrative and one of three bands. Teams are never ranked against one another, because team difficulty is not comparable. Individuals inside those teams are assessed separately on three axes — Own Contribution, Contribution to Others, and Trajectory — with explicit statistical correction for rater bias and an explicit confidence rating on every conclusion. No band may be lowered without passing a System Attribution Gate that asks whether the environment, not the person, produced the result.

Detail follows.

### 6.1 Layer 1: what is sensed, continuously

#### 6.1.1 The Contribution Ledger

An append-only, employee-owned record. Its purpose is to convert assessment from **recall** into **retrieval**.

- **Auto-populated** from the systems where work already leaves traces: merged changes, design documents, decision records, incident timelines, closed customer issues, shipped experiments, published research, deals, escalations resolved.
- **Manually appended** by the employee at any time — one line, thirty seconds: *"what I'd want remembered about this."* Especially for work that leaves no digital trace: the conversation that unblocked another team, the design someone talked out of a bad direction, the incident that never happened.
- **Appended by others**: peer recognition (§8.2) and Signal Pulse free-text land here automatically.

**Rules.**

1. The ledger belongs to the employee. Nothing may enter the judgment layer that the employee cannot see.
2. Ledger *volume* is never a metric. A prolific ledger and a sparse one are both fine; the ledger is a retrieval aid, not a scoreboard. (Volume-as-metric is the obvious Goodhart failure here, and it is closed explicitly.)
3. The ledger replaces the promotion packet entirely. Nobody at Meridian writes a document arguing for their own promotion.

#### 6.1.2 Signal Pulses

Fired **on completion of a meaningful unit of work** — a project, a launch, a quarter of sustained collaboration, a major incident — not on a calendar. Sent to the team lead and to 2–4 people who actually worked with the person. Under 90 seconds.

Five items. Four are statements about the **rater's own intentions or behavior**, per P4. One is a counterfactual.

| # | Item | Scale | What it is for |
|---|---|---|---|
| 1 | *Knowing what I know now, I would choose this person again for work like this.* | 1–5 | Overall behavioral intention — the highest-reliability single item available |
| 2 | *I would trust this person as DRI on something consequential, without supervision.* | 1–5 | Trust and scope — the real content of "seniority" |
| 3 | *If this person had not been on this work, the outcome would have been materially worse.* | 1–5 | **Counterfactual contribution** — the closest available proxy for marginal value |
| 4 | *This person made the people around them better.* | 1–5 | The anti-stack-rank axis; funds collaboration explicitly |
| 5 | *One thing that would raise this person's ceiling:* | free text | The only developmental item; goes straight to the person |

Item 5 is delivered to the person **immediately and unaggregated**. Items 1–4 are aggregated and used only in Layer 2. Item 3 is the item I have not seen in production anywhere, and it earns its place: it is the only question that asks about *marginal* contribution rather than absolute presence, which is the actual economic question.

#### 6.1.3 Team Telemetry

Reviewed weekly by the team, aggregated for assessment. Every outcome metric is deployed with a **paired guardrail it may not degrade** (P6).

| Metric | Paired guardrail | Why the pair |
|---|---|---|
| Delivery throughput | Change failure rate; defect escape rate | Speed bought with quality is a loan, not a gain |
| Outcome metric (team-specific) | The nearest downstream metric it could cannibalize | Local optimization at another team's expense |
| Incident response time | Incident *classification* accuracy | Fast response is trivially gamed by under-declaring |
| Customer resolution volume | Repeat-contact rate | Closing tickets ≠ solving problems |
| Cost efficiency | Sustainability index (on-call load, out-of-hours work, unplanned overtime) | Efficiency extracted from people is borrowed, not earned |

Plus a quarterly, anonymous, five-item **Team Health instrument**, adapted from Aristotle's five dynamics and Deloitte's three predictive items, reported **only at team level and only when n ≥ 5**:

1. *On this team, I can raise a problem or admit a mistake without it being held against me.* (psychological safety)
2. *I can count on my teammates to deliver what they say they will.* (dependability)
3. *I know what is expected of me and how my work is judged.* (structure and clarity)
4. *The work I do matters to something I care about.* (meaning and impact)
5. *I get to use my strengths most days.* (strengths fit — Deloitte's highest-correlating item)

#### 6.1.4 The cost meter

Hours consumed by Layer 1 are logged and reported to Layer 4 against the 0.9% cap (P13).

### 6.2 Layer 2A: the team assessment

Twice yearly. Assessed by the team lead and the lead's manager jointly, with input from the team's top three dependency partners (identified from the dependency graph, not chosen).

#### The five dimensions

| Dimension | The question | Evidence |
|---|---|---|
| **1. Outcome** | Did the team move the thing it exists to move? | Outcome metrics + guardrails; shipped work; customer/business effect |
| **2. Reliability** | Did the team do what it said, and did it say true things about what it could do? | **Forecast calibration** — the accuracy of the team's own commitments over time, not just its hit rate |
| **3. Leverage** | How much better were *other* teams' outcomes because of this team? | Dependency-weighted: input from dependent teams; reusable capability produced; blockers removed |
| **4. Health** | Is this team sustainable and safe? | Team Health instrument; on-call load; unplanned out-of-hours work; regretted attrition; time-to-productivity for new members |
| **5. Learning rate** | Is the team getting better at its own work? | Trend in cycle time and defect rate; postmortem action closure; capabilities added; documented reversals of prior decisions |

**Dimension 2 deserves comment.** Most organizations measure whether a team hit its commitments, which rewards sandbagging. Meridian measures **calibration**: a team that says "70% confident" and lands 70% of such calls is performing perfectly, while a team that hits 100% of its commitments is under-committing and is told so. This makes honest forecasting the winning strategy, which is the only way to get a planning system that produces information.

**Dimension 3 deserves comment too.** Leverage is where the platform team, the reliability team, the design system team and the internal tools team finally become measurable. In outcome-only systems these teams are permanently disadvantaged because their value appears on someone else's ledger. Weighting by dependency graph puts it back on theirs.

#### Output

A **written narrative** (one page, free-form, per Apple's discipline of forcing reasons rather than numbers) plus one of three bands:

| Band | Meaning | Consequence |
|---|---|---|
| **Compounding** | Delivering, and getting structurally better; other teams benefit | Increased autonomy and scope; first call on discretionary investment; team-level reward (§8.4) |
| **Delivering** | Doing the job it exists to do | Continue; specific improvement focus named |
| **Struggling** | Not delivering, or delivering unsustainably | **Triggers a system diagnosis, not a people action** |

**Teams are never ranked against each other.** A team maintaining a fifteen-year-old billing system and a team building a greenfield product face incomparable difficulty. Ranking them measures their assignment, not their performance.

#### The System Attribution Gate (P8)

Before any team may be banded **Struggling**, the assessing leaders must answer five questions in writing, and the answers are published to the team:

1. **Staffing** — was the team resourced to the level the work required?
2. **Dependency drag** — what fraction of the team's cycle time was spent blocked on others?
3. **Goal churn** — how many times did the team's objectives change mid-cycle?
4. **Tooling and environment** — did the team have what it needed to do the work?
5. **Clarity** — could the team state, at the start, what success looked like?

**If two or more come back red, the band is not applied to the team.** The finding is recorded as an *organizational* failure and remediation is assigned upward. This single gate is the mechanism that stops the oldest and most damaging pattern in performance management: an organization creating conditions in which no one could succeed, and then finding a person to hold responsible for the failure.

### 6.3 Layer 2B: the individual assessment

Twice yearly, running alongside the team assessment.

#### The three axes

Adapted from Microsoft's structure, which is the best individual model in the survey.

| Axis | The question | Weight |
|---|---|---|
| **A. Own contribution** | What did you do, and how good was it? | Judged by a domain-qualified evaluator (P10) |
| **B. Contribution to others** | What did you make possible for other people and teams? | Equal weight to A — deliberately |
| **C. Trajectory** | Is your capability compounding? Are you operating above your current level? | Forward-looking; separate from A and B |

Axis B carries equal weight to A by design. In most organizations it is a footnote, which is why senior people hoard context and avoid mentoring — the system does not pay for it. If teams produce the value (§2.3), then making the team better *is* the work, not a citizenship bonus on top of it.

#### Inputs

| Input | Source | Weight |
|---|---|---|
| Contribution Ledger | Continuous, employee-owned | Primary evidence base |
| Aggregated Signal Pulses | 4–8 raters per cycle, rater-corrected | Primary quantitative signal |
| Manager narrative | Team lead, written | Interpretive synthesis |
| Peer reviews | **2 self-selected + 2 assigned** | The assigned pair come from the dependency graph |
| Self-assessment | Employee, written | Framed as *"what should I do differently"*, never as advocacy |

**Why two assigned peers.** Purely self-selected reviewers produce a friendly sample and measure popularity. Assigning two reviewers from the people who actually depend on your output measures whether you are good to depend on — which is what colleagues actually need to know.

#### Rater fingerprinting and correction

This is the direct engineering response to §2.1, and it is the piece almost no organization implements.

Every rater is itself an instrument with a characteristic bias. Across all ratings a person has ever given, Meridian estimates:

- **Leniency** — their mean, relative to the global mean
- **Spread** — their standard deviation (does this person use the whole scale, or only 4 and 5?)
- **Halo** — the correlation among their own items (do they distinguish between the four questions, or give the same number four times?)
- **Agreement** — how well their ratings correlate with other raters of the same people

Scores are **standardized within rater** before aggregation, so a 4 from a severe rater and a 5 from a lenient one are read correctly. Raters with degenerate distributions — everyone gets a 5, or all four items always match — are **flagged, down-weighted, and coached**, because they are supplying no information. Aggregate rater-reliability statistics are published annually (P11, P12).

This does not eliminate rater variance. Nothing does. It converts a known, large, systematic error from something the system ignores into something the system corrects for and reports.

#### Output: a narrative, a coarse band, a confidence rating, and two flags

**A written narrative** — the primary output, structured to A/B/C, specific and evidence-linked.

**One of four bands** (P2 — four, because the instrument does not support more):

| Band | Meaning |
|---|---|
| **Exceptional** | Performing well beyond the expectations of the level, with evidence from multiple contexts |
| **Strong** | Doing the job of the level well. **This is the expected state for most people and is stated as such, out loud, permanently.** |
| **Developing** | Not yet at level — normal for someone new to a level, role or domain; a support plan, not a warning |
| **Off-track** | Sustained shortfall at level after the System Attribution Gate has been passed. Triggers §7.4. |

**A confidence rating — High / Medium / Low.** This is unusual and it is one of the design's most important features. Confidence is a function of evidence volume, rater count, rater agreement, and how much of the cycle the assessor actually observed.

> **The Low-Confidence Rule: a Low-confidence *Off-track* or *Developing* band cannot trigger any consequence.** It triggers one further cycle with deliberately increased evidence collection. If the instrument does not know, the organization does not act.

Almost every performance system in existence reports a point estimate from a noisy instrument with no error bar and then acts on it as though it were precise. Making uncertainty a first-class, published output is the honest engineering response to §2.1, and it costs the organization only the cases it was going to get wrong anyway.

**Two independent flags**, separate from the band because they are separate questions:

- **Promotion-ready** — operating at the next level (see §7.1)
- **Retention risk** — likely to leave, and we would regret it (see §8.1)

#### Calibration

Cross-team, twice yearly, run by domain-qualified leaders (P10), under three hard rules:

1. **No distribution target of any kind** (P3). The room may not ask "how many Exceptionals do we have?"
2. **A band may be moved only against written evidence, and that evidence is given to the employee.** Nothing decided in a calibration room may remain invisible to its subject.
3. **Every session's inputs and outcomes are logged and audited** for demographic skew, manager skew, team skew and tenure skew (P11, Layer 4).

### 6.4 Cadence summary

| Activity | Frequency | Hours per person per cycle | Stakes |
|---|---|---|---|
| Ledger append | Continuous, ad hoc | ~1.5/yr | None |
| Signal Pulse (as rater) | Per unit of work, ~6/yr | ~0.2 each ≈ 1.2/yr | None |
| Team Telemetry review | Weekly, in existing team meeting | 0 marginal | None |
| Team Health instrument | Quarterly | ~0.3/yr | None (team-level only) |
| Peer reviews (writing 4) | 2×/yr | ~3/yr | Indirect |
| Self-assessment | 2×/yr | ~2/yr | Indirect |
| Assessment conversation | 2×/yr | ~3/yr | High |
| Manager writing + calibration | 2×/yr | ~4/yr per report (manager cost) | High |
| **Total** | | **≈ 15 hrs/person/yr** | Within the 0.9% cap |

### 6.5 Worked example

*A staff engineer on the Platform team, second half of the year.*

**Team assessment (Platform).** Outcome: shipped the migration, 6 weeks late. Reliability: forecast calibration good — the team said 60% by Q3 and it landed in Q4, so the estimate was honest even though the date slipped. Leverage: **high** — four dependent teams report materially faster delivery post-migration; this is the team's strongest dimension and would be invisible in an outcome-only system. Health: on-call load elevated, safety score 4.1/5, one regretted departure. Learning rate: cycle time improved 22%, postmortem actions 80% closed. **Band: Compounding.** Narrative notes the on-call load as an organizational debt to be paid down, assigned to the Director, not the team.

**Individual assessment.** Axis A: led the migration design; two reversals of her own earlier decisions documented in the ledger, both caught early — read as strength, not weakness, per P9. Axis B: two engineers on adjacent teams cite her as the reason they could ship; she wrote the runbook the whole org now uses. Axis C: operating at the next level in one context, not yet in two.

Signal Pulses: 7 raters, rater-corrected mean 4.6; item 3 (counterfactual) is her highest at 4.9 — the strongest possible statement that her presence changed the outcome. Rater agreement high.

**Band: Exceptional. Confidence: High.** (7 raters, strong agreement, dense ledger, full-cycle observation.) **Promotion-ready flag: not yet** — one context, not two (§7.1). **Retention risk: elevated** — flagged to Layer 3, which triggers a Re-recruitment Review (§8.1) that finds her 12% under personal market and corrects it *before* she has to ask.

That last step is the whole design in miniature: the system noticed, and the organization acted, without requiring the employee to threaten to leave in order to be paid correctly.

---

<a name="7-question-2"></a>

## 7. Question 2 — The strategic elevation plan

> *"What is your strategic elevation plan?"*

**Short answer.** Elevation operates at three levels that most organizations conflate: **individuals** rise through a published ladder defined by the ambiguity they can absorb, with promotion recognizing a level already being performed in two distinct contexts. The **organization** raises its own capability through an explicitly-owned Capability Map with maturity targets, bench-depth requirements, and a protected 15% capacity allocation — because individual growth does not automatically compound into organizational capability. And **strategy is translated into measurement annually**, because a strategy that does not change what gets measured will not happen.

### 7.1 Individual elevation

#### The ladder is defined by ambiguity absorbed, not by years or headcount

| Level | Defining question: what can you be handed? | Judgment blast radius |
|---|---|---|
| **L1 — Assisting** | A well-defined task, with the approach given | Your own work, reviewed |
| **L2 — Executing** | A well-defined problem; you choose the approach | Your own work |
| **L3 — Owning** | An ambiguous problem in a known domain; you define and deliver it | Your team's near-term outcomes |
| **L4 — Leading** | An ambiguous problem spanning teams; you find the right problem, not just the right solution | Multiple teams; one quarter to one year |
| **L5 — Shaping** | A domain with no defined problem; you decide what should be worked on | The organization; one to three years |
| **L6 — Setting direction** | A strategic frontier; you change what the organization believes is possible | The company; multi-year |

Management runs as a **parallel track with equal ceilings and equal pay bands.** Managing people is a different job, not a higher one. Movement between tracks in both directions is normal and is not recorded as a demotion — a rule that has to be enforced explicitly, because the default culture will read it as one.

Every level is published with three or four real, anonymized examples of work at that level, refreshed annually. This is the single cheapest intervention against §3.4's opacity problem: people can only aim at a target they can see.

#### The promotion rule

> **Promotion recognizes a level you are already operating at, demonstrated across two assessment cycles and two distinct contexts.**

Three deliberate properties:

- **Already operating at.** Promotion is a recognition of fact, not a bet. This removes the "prove you can do it after we promote you" dynamic that produces failed promotions and quiet demotions.
- **Two cycles.** Filters single-quarter luck.
- **Two distinct contexts** — different problem, different collaborators, or different manager. This is the one that matters most, because it directly attacks the §2.1 problem: a single manager's high opinion is not evidence of a level, it is one measurement from one instrument. Two contexts requires the signal to survive a change of instrument.

**No promotion packet.** The Contribution Ledger is the evidence. Nobody at Meridian spends three weeks writing a document arguing for themselves — which is a tax paid disproportionately by people who are less comfortable with self-advocacy, and which distorts work selection toward the legible for months beforehand (§3.1).

#### Demand-anchored, not quota-capped

Promotions are **not** capped by a budget quota. But higher levels require scope that genuinely exists — you cannot be L5 if there is no L5-sized problem, because the level is defined by the problem, not the person.

This creates an honest obligation running the other way:

> **The Scope Obligation.** If a person is assessed promotion-ready and no scope exists at that level, the organization has **two quarters** to create the scope, or it must tell the person plainly: *"You are ready, we do not have the room, here is what we are doing about it, and we understand if you leave."*

Most organizations handle this by manufacturing a reason the person is not quite ready — which is a lie that costs the organization its credibility and usually the person as well. Saying the true thing costs less.

### 7.2 Organizational elevation

This is the level almost every performance system omits, and its omission is why organizations full of individually-improving people stay organizationally stuck. Individual growth does not automatically aggregate into organizational capability — capability lives in systems, documentation, tooling, standards and redundancy, none of which any individual is measured on.

#### The Capability Map

The 8–12 capabilities the strategy actually requires, each with a **named owner** (an accountable person, not a committee), a **current maturity level**, and a **target with a date**. Reviewed twice yearly at the executive level with the same seriousness as financial results.

| Maturity | Definition |
|---|---|
| **M1 — Individual** | One or two people can do this; it lives in their heads |
| **M2 — Repeatable** | Documented and reproducible; several people can do it |
| **M3 — Systematized** | Tooled, defaulted, hard to do wrong; new joiners inherit it |
| **M4 — Compounding** | The organization measurably improves at it without deliberate effort |

*Illustrative for Meridian:* incident response M3→M4; ML evaluation M1→M3 (strategic, currently a single point of failure); enterprise security review M2→M3; customer research synthesis M1→M2; multi-tenant data isolation M2→M3.

#### Bench Depth Ratio

For every critical capability and every critical role: **how many people could do this at level?** Target ≥ 2. A ratio of 1 is a named organizational risk with a named owner and a date, reported alongside the Capability Map. This converts key-person risk from a thing everyone privately knows into a thing the organization is accountable for.

#### The Strategy Delta Review

Once a year, after strategy is set, a mandatory review that produces three artifacts:

1. **Changed team outcome metrics** — which metrics are retired, which are added
2. **Changed capability targets** — what the strategy now requires that it did not
3. **Changed ladder examples** — what "excellent L4 work" now looks like, given the new strategy

> **The rule:** *if the strategy changed and none of the three artifacts changed, the strategy has not actually changed.* People optimize what is measured. A new strategy that leaves the measurement system untouched is a slide deck.

This review also executes the **metric sunset** from P6: every metric older than four cycles must be re-justified in this room or it is deleted. Metric sets grow monotonically in every organization that does not do this, and a metric set that only grows eventually measures nothing because attention is finite.

#### The protected elevation portfolio

**15% of organizational capacity is allocated to capability-building work with no near-term outcome metric** — platform investment, tooling, documentation, deliberate skill acquisition, research with uncertain payoff.

It is protected not by exhortation but by measurement: it is what the team assessment's **Learning Rate** dimension (§6.2) evaluates. Slack time that is not measured is the first thing consumed under deadline pressure, every single time. Making it an assessed dimension is what converts it from an intention into a commitment.

### 7.3 Mobility and succession

#### The Talent Export Credit

> **Managers are assessed, in their own Axis B, on the people they export who succeed elsewhere in the company.**

Every organization has a talent-hoarding problem, and it is not a character flaw — it is a rational response to an incentive. A manager who releases their best engineer loses output this quarter and gains nothing measurable, ever. So they block the transfer, or discourage it quietly, and the person eventually leaves the company instead of the team.

Crediting exports inverts the incentive at its source. A manager whose people are in demand elsewhere is a manager who develops people, and Meridian pays for that explicitly. The auditable version: track, per manager, the number of internal transfers out and the assessment band of those people **one year later** in their new team.

**Internal mobility mechanics:** all roles posted internally first for five days; no manager veto on a transfer, only a negotiated timeline capped at 90 days; a "tour of duty" option (three to six months, guaranteed return) that makes trying something new low-risk and therefore common.

#### Succession

Every role at L4 and above, and every M1-maturity capability, has **two named successors** classified *ready now* or *ready in 12 months*, with the development gap named for each. Reviewed twice yearly. A role with zero named successors is treated as an open organizational risk, not a fact of life.

### 7.4 Elevation for people who are struggling

Meridian **inverts** Microsoft's internal-transfer bar (§3.6). Poor fit is among the most common and cheapest-to-fix causes of low performance, and blocking the fix in the name of rigor is expensive theater.

An **Off-track** band with **High** confidence triggers this sequence, in this order, with the order being the point:

| Step | Question | Typical duration |
|---|---|---|
| **1. System diagnosis** | Did the environment cause this? (The System Attribution Gate, applied to the individual: staffing, dependencies, goal churn, tooling, clarity, manager availability.) | 2 weeks |
| **2. Fit review** | Is this the wrong role for a capable person? **Internal transfer is actively supported here**, with a warm introduction, not a bar. | 4 weeks |
| **3. Capability plan** | A specific, resourced, written plan with named support and a defined bar | One full cycle |
| **4. Exit with dignity** | Generous severance, honest reference, no stigma, no rehire ban | 2 weeks |

**Two hard guarantees, published:**

1. **No one is exited for performance without at least one prior assessment cycle in which they were told, in writing, exactly what was insufficient and given a real path.** Surprise is a management failure, and the organization absorbs the cost of its own failures rather than passing them to the person.
2. **No rehire ban and no transfer bar, ever.** People fail in roles and succeed in others; an organization that treats a bad fit as a permanent mark on a person is optimizing its own ego over its access to talent.

---

<a name="8-question-3"></a>

## 8. Question 3 — The recognition and reward system

> *"What is your recognition and reward system?"*

**Short answer.** Meridian pays in four distinct currencies, deliberately engineered to be separate because they run on different psychology and fail in different ways. **Money** is slow, coarse, market-anchored, and structurally decoupled from the rating — there is no individual performance bonus for most roles. **Recognition** is fast, peer-driven, public, and deliberately *non-convertible to cash*, because the moment recognition converts to money it becomes a currency to farm. **Opportunity** — access to consequential work — is treated as the highest-value reward there is and is explicitly measured and audited, because it is the reward that actually determines careers and the one every organization allocates by accident. And a portion of reward is **indivisible and team-level**, because divisible rewards for joint production are a lie about how the value was made.

### The premise: money and recognition are not the same instrument

Extrinsic reward tightly coupled to measured output has two well-established failure modes on complex cognitive work. It crowds out intrinsic motivation — the work becomes something you do for the payment, and interest in it declines. And beyond modest stakes it *degrades* performance: Ariely, Gneezy, Loewenstein and Mazar found that very large contingent bonuses reduced performance on tasks requiring cognitive skill rather than improving it.

Combine that with §2.1 — the instrument determining the bonus is majority noise — and the standard performance bonus is revealed for what it is: **a large, noisy, motivation-degrading payment that teaches people to manage their rating.** Netflix's answer, which Meridian adopts, is to pay well enough that money stops being a live question and then stop using money as a steering wheel.

### 8.1 Currency 1 — Compensation: slow, coarse, market-anchored, decoupled

| Component | Design | Why |
|---|---|---|
| **Base salary** | Set by level band × market data. **Bands published internally**, with the within-band distribution published. Position in band moves with sustained assessment band and level. | Transparency is the only real defense against unexplained disparity (P11) |
| **Individual performance bonus** | **None**, for the great majority of roles. That money is moved into base. | A bonus keyed to a majority-noise rating buys gaming, not effort |
| **Company profit share** | Uniform **percentage of base** for everyone, paid annually. | Same percentage for everyone means the same stake for everyone. The one thing genuinely collectively produced is company results. |
| **Equity** | Multi-year vesting, refreshed annually against level and sustained band. | The only instrument whose time constant matches long-horizon contribution |
| **Variable pay where it genuinely fits** | Some revenue roles have real, low-gaming, individually-attributable output. Commission is legitimate there — **with paired guardrails** (churn at 12 months, discount depth, implementation success) and a 12-month clawback window. | Don't apply a blanket rule where the underlying facts differ. Do apply P6. |
| **Annual equity sweep** | An automatic audit for unexplained pay gaps by demographic, tenure and manager, with a **budget reserved to correct them without anyone having to ask.** | Measuring a gap does nothing. Most systems have a measurement mechanism and no correction mechanism. |

#### The Re-recruitment Review — replacing the Keeper Test

Netflix's Keeper Test asks the right question and points it in the wrong direction. Meridian keeps the question and inverts the direction of consequence.

**Annually, for every employee, the manager answers two questions in writing:**

1. *If this person were on the open market today, what would we have to pay to hire them?*
2. *Would we?*

**Then the obligation falls on the organization, not the person.** If the answer to (1) exceeds current pay, the gap is closed or the manager explains — to the employee — why not. If the answer to (2) is no, that triggers §7.4's sequence, which begins with a system diagnosis and includes a supported internal transfer, not a severance conversation.

Compare the incentive structures. The Keeper Test makes an honest manager assessment *cost the employee their job*. The Re-recruitment Review makes it *cost the organization money*. Under the first, every manager has a standing incentive to find reasons to downgrade. Under the second, every manager has a standing incentive to find reasons to retain — and to say so before the person has to interview elsewhere to be paid correctly.

Same information. Opposite direction of pressure. The second one is also simply how the market works: people are paid what they can command, and pretending otherwise only means you find out at resignation.

### 8.2 Currency 2 — Recognition: fast, peer-driven, public, non-convertible

Recognition operates on status, belonging and mastery, not on the wallet. It is nearly free, effectively unlimited, and works on a timescale money cannot touch — the day the thing happened rather than eleven months later.

**Peer Recognition Grants.** Every employee receives a monthly allocation of recognition grants to give away.

| Rule | Reason |
|---|---|
| **Expires monthly, does not accumulate** | Forces use; a hoarded budget recognizes nobody |
| **Cannot be self-awarded** | Obvious |
| **Must name a specific artifact or behavior and one Operating Principle** | Vague praise ("great job!") carries no information and no reinforcement |
| **Public by default** | The payload is visibility, not the token |
| **Auto-appends to the recipient's Contribution Ledger** | Becomes evidence a human reads at review time — never a score that is counted |
| **Reciprocity decay** | Repeated A→B→A pairs count progressively less, which breaks mutual-admiration rings |
| **Per-pair quarterly cap** | Prevents concentration and log-rolling |
| **Never converts to cash and never enters a rating formula** | **The single most important rule.** A social currency convertible to money becomes a farmed currency within one quarter. |

**Non-cash payloads are fine and good:** a charity donation in the recipient's name, learning budget, conference attendance, a day off, dinner. What must not exist is a published exchange rate between recognition and compensation.

**The asymmetry rule.** Recognition is frequent, public, specific and generous. Criticism is private, specific and immediate — never saved up for a review. Feedback that has been stored for four months has lost its usefulness and gained only its sting.

**Anti-inflation.** There is a **cap** on how many top-tier awards exist per period, and no **floor**. If nothing exceptional happened this quarter, nothing is awarded. An award that is always given stops being an award, and everyone knows it before the organization admits it.

### 8.3 Currency 3 — Opportunity: the largest reward, and the one nobody measures

The most valuable thing an organization can give a person is not money. It is **the chance to work on something that matters, with people they learn from, where success is visible.** That is what actually compounds into a career.

And in almost every organization it is allocated by proximity, familiarity and similarity to the person doing the allocating — which is the primary mechanism by which advancement becomes unequal, operating entirely beneath the level at which anyone would recognize it as a decision.

Meridian therefore **measures opportunity allocation and publishes the distribution.**

| Opportunity reward | How it is allocated | How it is audited |
|---|---|---|
| **DRI on consequential work** | Named explicitly, with the assignment recorded | **Opportunity Share** report: distribution of high-visibility assignments by level, tenure, team, demographic |
| **Choice of next assignment** | Earned by sustained Strong+ band; a real, exercisable preference | Tracked: were preferences honoured? |
| **Budget and headcount authority** | Attached to scope, not to title | Published |
| **External visibility** | Conference talks, publications, open-source ownership | Distribution reviewed twice yearly |
| **Autonomy** | Reduced check-ins, direct decision rights | Explicitly granted and named, so it is a reward rather than an accident of manager style |
| **Time** | Sabbatical at 4 years; protected learning time | Uptake tracked (low uptake means it isn't real) |

**The Opportunity Share report is one of this design's more consequential features.** No organization I am aware of measures this, and it is where careers are actually made. Publishing it makes a previously invisible allocation visible, and visible allocations get argued about — which is exactly what should happen.

### 8.4 Currency 4 — Team rewards: indivisible on purpose

If value is produced jointly (§2.3), some reward must be indivisible, or the reward system is telling a lie about how the work happened.

- **Team celebration budget**, discretionary, no approval needed, spent by the team.
- **Compounding-band teams** receive a profit-share uplift shared **equally across every member**, including the people whose contribution was least visible.
- **Shipping rewards go to the whole team** — support, QA, documentation, operations, the person who did the migration nobody saw. The default failure is to reward the people who presented the launch.
- **A team that prevents a crisis is rewarded like a team that resolves one** — see below.

### 8.5 What Meridian deliberately does not reward

| Not rewarded | Why |
|---|---|
| **Hours, presence, responsiveness** | Measures compliance and availability, not contribution; taxes caregivers and anyone in an inconvenient time zone |
| **Heroics and firefighting** | Rewarding the fix while ignoring the prevention creates a reliable supply of fires. See the Prevention Credit below. |
| **Volume of output** | Trivially gamed; correlates with value only accidentally |
| **Any metric movable only by degrading a teammate's** | Manufactures internal competition in a joint-production system |
| **Being liked** | The hardest one, and the reason for rater correction, assigned peers, and the Opportunity Share audit |

#### The Prevention Credit

The prevention paradox: the best incident is the one that never occurred, and it is therefore invisible, unattributable and unrewarded. Every organization thus systematically overpays for firefighting and underpays for fire prevention, and then wonders why it has so many fires.

Meridian makes prevention **explicitly claimable**. Any person or team may log a **prevention claim** in the ledger: *"this class of failure was possible; here is the evidence it was possible; here is what we did; here is why it can no longer happen."* Claims are reviewed at assessment time as first-class contribution — weighted by the estimated severity and likelihood of what was prevented.

It is imperfect. Counterfactuals are unverifiable and the mechanism can be inflated. But the alternative is a system in which prevention is worth *exactly zero*, and a noisy positive number beats a precise zero when the precise zero is known to be wrong. The Signal Pulse counterfactual item (§6.1.2) is the individual-level version of the same correction.

---

<a name="9-added-features"></a>

## 9. Added features: the twelve differentiators

Consolidated, with what each fixes. These are the elements not found in the systems surveyed in §3.

| # | Feature | The problem it fixes | Where |
|---|---|---|---|
| **1** | **Confidence-rated assessments** with the Low-Confidence Rule | Point estimates from noisy instruments treated as precise | §6.3 |
| **2** | **System Attribution Gate** | Organizations create conditions where no one can succeed, then blame a person | §6.2, §7.4 |
| **3** | **Rater fingerprinting and standardization** | 53–62% of rating variance is the rater, and nobody corrects for it | §6.3 |
| **4** | **Counterfactual pulse item** | Presence is measured; *marginal contribution* is the actual question | §6.1.2 |
| **5** | **Forecast calibration as a team dimension** | Hit-rate targets reward sandbagging; calibration rewards honesty | §6.2 |
| **6** | **Dependency-weighted Leverage** | Platform and enablement teams' value lands on someone else's ledger | §6.2 |
| **7** | **Talent Export Credit** | Talent hoarding is rational under every conventional system | §7.3 |
| **8** | **Opportunity Share audit** | The reward that most determines careers is allocated invisibly | §8.3 |
| **9** | **Prevention Credit** | Prevention is worth exactly zero in every outcome-based system | §8.5 |
| **10** | **Re-recruitment Review** | Keeper Test's information without its fear; inverts who bears the cost of candor | §8.1 |
| **11** | **Metric sunset + adversarial red-teaming** | Metric sets grow monotonically and decay under Goodhart | §7.2, below |
| **12** | **Layer 4 meta-measurement** | Performance systems are almost never tested for predictive validity | below |

### Feature 11 detail — Red-teaming the metric set

Before any metric is deployed, a group that does not own it must answer, in writing: **"How would I move this number without doing the underlying job?"** Any answer that is cheaper than doing the job disqualifies the metric or mandates a guardrail. Repeated annually at the Strategy Delta Review, because gaming strategies are discovered over time and a metric that was safe in year one is often compromised by year three.

### Feature 12 detail — Layer 4: the system measures itself

Published internally every year. A performance system that produces no evidence about its own accuracy is a ritual, and rituals do not improve.

| Meta-metric | Question | Action threshold |
|---|---|---|
| **Predictive validity** | Do this year's bands predict next year's outcomes, peer assessments, and retention better than chance? | If not materially better than chance, the banding is scrapped |
| **Rater reliability** | Inter-rater agreement; % of raters flagged degenerate | Declining agreement → retrain or narrow the rater pool |
| **Distribution audit** | Band, promotion, pay and Opportunity Share distributions by demographic, tenure, team, manager | Any unexplained skew is investigated with a named owner and a date |
| **Assessment stability** | How often does a person's band swing two levels between cycles? | High volatility means we are measuring noise |
| **System cost** | Hours consumed as % of working hours | Cap 0.9%; exceeding it forces removal of a component |
| **Trust** | *"I believe this system assesses me fairly."* — measured anonymously | Below 60% agreement is a redesign trigger, not a communications problem |
| **Gaming detection** | Anomaly scan: metric spikes near cycle boundaries; recognition-token clustering; ledger stuffing | Named and closed publicly |
| **Regretted attrition among Exceptional/Strong** | Are we losing the people the system says are best? | The most important number in the table |

That last row deserves the final word. If an organization's performance system identifies its best people and then loses them, every other number in the system is decoration.

---

<a name="10-failure-modes"></a>

## 10. Failure modes and the defenses against them

Designed defensively: for each known failure mode, the mechanism that produces it, the defense, and the meta-metric that detects the defense failing.

| Failure mode | Mechanism | Defense in this design | Detector |
|---|---|---|---|
| **Ratings measure the manager** | Rater idiosyncrasy (§2.1) | Rater fingerprinting; 4–8 raters; 2 assigned peers; calibration; two-context promotion rule | Rater reliability; assessment stability |
| **Goodhart decay** | Stakes attached to a gameable metric | Paired guardrails; red-teaming; metric sunset; zero-stakes sensing layer | Gaming detection scan |
| **Blaming people for system failures** | Attribution error under pressure | System Attribution Gate, mandatory and published | % of Struggling bands reversed at the gate |
| **Talent hoarding** | Manager loses output by releasing people | Talent Export Credit in Axis B; no transfer veto | Internal transfer rate; exported-talent success at 12 months |
| **Invisible work goes unpaid** | Only legible work reaches the assessor | Contribution Ledger; Prevention Credit; Leverage dimension; counterfactual item | Band distribution across enablement vs. product teams |
| **Recognition inflation** | Everyone awarded, award becomes noise | Cap with no floor; non-convertible tokens; reciprocity decay | Token distribution Gini; % receiving top awards |
| **Bias in advancement** | Opportunity allocated by proximity and similarity | Opportunity Share audit; published ladders and criteria; calibration audit | Distribution audit |
| **The system eats the work** | Process accretion; nobody ever deletes | 0.9% hours cap; every addition must name a removal | System cost |
| **Long-horizon work punished** | Six-month cycle with money attached | Money decided annually; equity multi-year; Prevention Credit; Learning Rate dimension | Assessment bands for research/platform roles |
| **Regression to punitive measurement under margin pressure** | Quotas look decisive and are cheap | P3 written as a constitutional rule with the §3.6 evidence attached; Layer 4 published to the whole company | Trust metric; any proposal for a quota |
| **Feedback stops being honest** | Stakes leak into the sensing layer | Layer 1 never converts directly to money; pulse item 5 goes only to the person | Trust metric; pulse score inflation over time |
| **Assessment becomes an annual surprise** | Deferred conversations | Two hard guarantees (§7.4); continuous pulse delivery | % of Off-track bands with no prior written warning — target zero |

---

<a name="11-what-this-system-refuses-to-do"></a>

## 11. What this system refuses to do

Stated explicitly, because a design is defined as much by its exclusions, and because these are the things that will be proposed again the first time margins tighten.

1. **No forced distribution, curve, quota, or bottom bucket.** Microsoft ran it and abandoned it as harmful (§3.6). Applied to a majority-noise instrument, a bottom-bucket quota selects on rater severity and team difficulty, not performance.
2. **No target for how many people should leave.** Amazon's URA (§3.2) sets the answer before collecting the data. It also makes defensive hiring rational, which is disqualifying on its own.
3. **No composite numeric score.** No 3.7 out of 5. The instrument does not support that precision, and false precision produces false confidence in exactly the decisions that need humility.
4. **No annual-only cycle.** Feedback delayed eleven months is not feedback.
5. **No 360 feedback tied directly to pay.** It converts honest peer input into political currency within one cycle.
6. **No promotion packet.** It taxes self-advocacy unequally and distorts work selection for months (§3.1).
7. **No rehire bans and no transfer bars.** They optimize the appearance of rigor over the economics of talent (§3.6).
8. **No engagement score as a headline KPI.** A single satisfaction number is optimized by managers rather than improved, and it tells you nothing actionable. Meridian measures the five specific team-health items instead.
9. **No secret criteria.** Everything except individual pay is published. Unauditable systems accumulate bias without anyone intending it.
10. **No rating abolition.** Deleting the rating does not delete the judgment; it only makes it invisible and unchallengeable (§3.7).

---

<a name="12-cost-model-and-scaling"></a>

## 12. Cost model and scaling

### Cost at 450 people

| Component | Hours/person/yr | Total hours | Notes |
|---|---|---|---|
| Layer 1 sensing | 3.0 | 1,350 | Mostly seconds-at-a-time |
| Layer 2 peer + self writing | 5.0 | 2,250 | Twice yearly |
| Layer 2 assessment conversations | 3.0 | 1,350 | Both parties |
| Manager writing + calibration | 3.5 | 1,575 | Concentrated on ~60 managers |
| Layer 3 + Layer 4 | 0.5 | 225 | Centralized |
| **Total** | **≈15** | **≈6,750** | **≈0.78% of working hours** |

For comparison: Deloitte measured its pre-redesign system at roughly 2 million hours per year, and Adobe recovered 80,000–100,000 manager hours annually by replacing its annual review. The cap is not decoration — it is the constraint that forces every proposed addition to displace something.

### Scaling

| Size | What changes |
|---|---|
| **~50** | Drop formal calibration (one room holds everyone) and the Capability Map's formality. Keep: ledger, pulses, published ladder, decoupled pay, System Attribution Gate. Rater correction is not yet statistically meaningful — compensate with more raters per person. |
| **~450 (design point)** | As specified. |
| **~2,000** | Calibration becomes multi-level; rater fingerprinting becomes statistically strong; Layer 4 needs a dedicated analyst. Add explicit cross-org calibration audits. |
| **~10,000+** | The main risk is that Layer 3 begins reaching back into Layer 2 to fit budgets — Google's failure mode (§3.1). Defense: make P3 a published constitutional rule with an executive owner, and publish the Layer 4 distribution audit company-wide so a violation is visible to everyone. |

---

<a name="13-implementation-roadmap"></a>

## 13. Implementation roadmap, with kill criteria

Rolled out as an experiment with a control group, because a performance system that has not been tested is an assertion.

| Phase | Window | What happens |
|---|---|---|
| **0. Baseline** | Weeks 1–4 | Measure the current state *before* changing anything: trust, cost in hours, band/pay/promotion distributions, regretted attrition, current rater agreement. Without a baseline, no later claim about the new system is checkable. |
| **1. Foundations** | Weeks 5–12 | Publish the ladder with real examples. Publish pay bands. Write the Operating Principles. Build the Contribution Ledger (integrations first, manual entry second). Train managers on the System Attribution Gate. |
| **2. Pilot** | Weeks 13–26 | Three teams (~40 people) run the full system. Three matched teams continue as-is. Compare on trust, cost, band stability, and manager time. |
| **3. Sensing everywhere** | Weeks 27–39 | Signal Pulses, Team Telemetry with guardrails, and Peer Recognition Grants go org-wide. **Zero stakes attached** — a full cycle of data before anything counts. |
| **4. Judgment layer** | Weeks 40–52 | First full team and individual assessments. First calibration. First Layer 4 report published, including the pilot-vs-control comparison. |
| **5. Consequence layer** | Year 2, Q1 | Compensation moves to the new model. Re-recruitment Reviews run. Equity sweep executes. **Money changes last, deliberately** — after a full year of evidence, so the first real assessment is not also the first real payout. |
| **6. Organizational elevation** | Year 2, ongoing | Capability Map, Bench Depth, Strategy Delta Review, Opportunity Share reporting. |

### Kill criteria

Stated in advance, because a design that cannot be killed will be defended past its usefulness.

Scrap or substantially rebuild if, after two full cycles:

- **Trust** in the system is below 60% and not improving;
- **Predictive validity** of bands is not materially better than chance;
- **Cost** exceeds 1.2% of working hours;
- **Regretted attrition among top-banded employees rises** relative to baseline;
- Managers report they are **routing around** the system to get outcomes they want — the clearest possible signal that the formal system has become theater.

---

<a name="14-honest-limitations"></a>

## 14. Honest limitations

Where this design is weak, stated plainly.

1. **The Contribution Ledger can become performative.** If people learn that a dense ledger reads well, it becomes a self-promotion feed and re-imports the promotion-packet problem it was built to remove. Mitigations — volume is explicitly never a metric, assessors are trained to weight evidence quality over quantity, auto-population dominates manual entry — reduce this but do not eliminate it. **Watch it in Layer 4 from cycle one.**

2. **Rater fingerprinting needs volume.** With fewer than roughly 20 ratings per rater, leniency and spread estimates are themselves noisy. Below ~150 people, use it as a diagnostic and coaching tool rather than a correction factor, and lean harder on rater count per person.

3. **Confidence ratings can become an excuse for indecision.** "Low confidence" is available to a manager who does not want a hard conversation. Countermeasure: Layer 4 tracks the rate of Low-confidence assessments *per manager*, and a manager who never reaches High confidence about anyone is themselves the finding.

4. **P10 — expert evaluators — is a genuine constraint, not a preference.** It restricts who can manage, and it conflicts with the common practice of promoting generalist managers into domains they cannot read. Where the org cannot satisfy it, the fallback (technical assessment sourced from a qualified peer) is real but weaker, and it should be recorded as capability debt on the Capability Map rather than quietly accepted.

5. **This design assumes a floor of good faith.** In a genuinely low-trust organization, the ledger becomes a defensive record, pulses become retaliation, and the Re-recruitment Review becomes a device for identifying who is cheap to lose. **No measurement system repairs a broken culture; measurement systems amplify whatever culture already exists.** If trust is already below the kill threshold on day one, fix that first — this design is not the tool for it, and deploying it into that environment will make things worse rather than better.

6. **The Prevention Credit is unfalsifiable by construction.** Counterfactual claims cannot be verified. It is included because the alternative — valuing prevention at exactly zero — is a *known* error, and a noisy correction beats a precise wrong answer. But it will be inflated by some people, and the review of prevention claims needs to be genuinely skeptical.

7. **Removing individual bonuses will be unpopular with a specific group** — high performers accustomed to large variable pay, and candidates comparing offers against companies that lead with bonus numbers. The compensating higher base is economically equivalent or better in expectation, but it is less exciting to talk about, and recruiting will feel it. That cost is real and is accepted deliberately.

8. **Everything here is a design, not a result.** The components draw on published evidence, but the *combination* has not been tested. Section 13's control group and Section 4's P12 exist precisely because this document should not be believed on its own authority. It should be measured.

---

<a name="sources"></a>

## Sources

**Research**

- Scullen, S. E., Mount, M. K., & Goff, M. (2000). *Understanding the latent structure of job performance ratings.* Journal of Applied Psychology — [Semantic Scholar](https://www.semanticscholar.org/paper/Understanding-the-latent-structure-of-job-ratings.-Scullen-Mount/0a73fb7d291a407656d4ee4a9b1eb19514abe157)
- [Manifestation of idiosyncratic rater effect in employee performance appraisal](https://businessperspectives.org/images/pdf/applications/publishing/templates/article/assets/13975/PPM_2020_03_Paramesh.pdf) — Problems and Perspectives in Management
- Buckingham, M., & Goodall, A. (2015). [Reinventing Performance Management](https://hbr.org/2015/04/reinventing-performance-management) — Harvard Business Review
- [Understand team effectiveness (Project Aristotle)](https://rework.withgoogle.com/intl/en/guides/understand-team-effectiveness) — Google re:Work
- [Google's Project Aristotle](https://psychsafety.com/googles-project-aristotle/) — Psych Safety
- [How Apple Is Organized for Innovation](https://www.apple.com/careers/pdf/HBR_How_Apple_Is_Organized_For_Innovation-4.pdf) — HBR, hosted by Apple

**Company practice**

- [Google overhauls performance ratings to sharpen focus on high achievers](https://www.hrkatha.com/news/google-overhauls-performance-ratings-to-sharpen-focus-on-high-achievers/) — HRKatha
- [Google's New Performance Review System Promises Huge Bonuses For High Achievers](https://allwork.space/2025/04/googles-new-performance-review-system-promises-huge-bonuses-for-high-achievers/) — Allwork
- [Understanding Amazon Forte & OLR Performance Review](https://agilityportal.io/blog/understanding-amazon-forte-olr-performance-review) — AgilityPortal
- [Leaked Amazon memo shows how it forces out employees to hit targets](https://www.hcamag.com/us/news/general/leaked-amazon-memo-shows-how-it-forces-out-employees-to-hit-targets/253161) — HRD
- [Netflix CTO says the company has no 'formal performance reviews'](https://www.yahoo.com/news/articles/netflix-cto-says-company-no-165053459.html) — Yahoo/Business Insider
- [How Netflix does Performance Management, 360 Feedback, & Rewards](https://www.performyard.com/articles/how-netflix-does-performance-management) — PerformYard
- [How Apple Does Performance Management](https://www.performyard.com/articles/apple-performance-management) — PerformYard
- [Meta is about to start rating more workers as 'below expectations'](https://www.aol.com/news/meta-start-rating-more-workers-150352928.html) — Business Insider via AOL
- [Microsoft Sets Tougher Rules for Underperformers, Adds Two-Year Rehire Ban](https://finance.yahoo.com/news/microsoft-sets-tougher-rules-underperformers-165952780.html) — Yahoo Finance
- ['Stack Ranking' Ends at Microsoft, Generating Heated Debate](https://www.shrm.org/topics-tools/news/benefits-compensation/stack-ranking-ends-microsoft-generating-heated-debate) — SHRM
- [How Adobe Scrapped Its Performance Review System And Why It Worked](https://www.forbes.com/sites/davidburkus/2016/06/01/how-adobe-scrapped-its-performance-review-system-and-why-it-worked/) — Forbes
- [Why Adobe killed off the annual performance review](https://www.managers.org.uk/knowledge-and-insights/case-study/why-adobe-killed-off-the-annual-performance-review/) — CMI

---

*Meridian Performance System v1.0 — a design to be measured, not believed.*
