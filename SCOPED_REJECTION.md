# Scoped Rejection with Contestable Dependency Closure

**Status: PUBLISHED CANDIDATE surface — not a confirmed component of any
system. Maturity: operator-derived, operationally exercised,
externally unvalidated. Deliberately small: one mechanism, three parts.**

Provenance of this text: it passed a multi-round external adversarial
review gate (round 1: two independent reviewers in parallel; rounds 2-3:
two further reviewer lineages; final round verdicts drove the last
revisions) across 2026-08-21/22. Its claims of absence are bounded to
documented search scopes.
## The problem this names

In mainstream CODE review, one reviewer's objection to one part freezes
the whole; document tooling does have section-level approval (page-
section approval macros in wiki tooling; clause-conditional approval
routing in contract-management suites; a published patent with
per-section approval states on a workflow graph, US20180300304A1) —
acknowledged, and distinguished below: none of those systems propagates
a rejection along a semantic dependency map, and none makes the map
contestable. In code review the freeze is near-universal: GitHub's request-changes blocks the entire pull
request; Gerrit's −2 blocks the change; an IESG DISCUSS names specific
issues yet still holds the entire document — the objection is scoped, the
BLOCKING is not. In high-throughput multi-agent work this converts every
localized finding into a global stall: one defect in one section parks
ten sections of unrelated, finished work.

## What this document claims

Scoped rejection with a landing remainder is OLD outside software:
line-item veto lets named items fall while the remainder becomes law;
parliamentary division of the question votes severable parts separately;
in document tooling, per-section approval exists without dependency
semantics (above); and in code review, stacked-change systems (Gerrit relation chains,
Depends-On footers) land unrelated stack members while a −2 blocks
exactly the declared dependents — an author-declared, discussion-
contestable dependency graph at CHANGE granularity. All acknowledged.
The claim, re-scoped precisely: within a documented search scope
(English-language web, arXiv, platform documentation, surveyed
2026-08-21, medium depth, recorded queries), no public review system
provides this WITHIN A SINGLE ARTIFACT at SECTION granularity over
SEMANTIC dependencies — where the dependency map is not a commit graph
or a build graph but a contestable claim about meaning, published by the
author as a first-class review object. That narrower composite is the
stake.

## The mechanism (three parts)

1. **A rejection carries scope.** A REJECT names the sections it blocks.
   Its blast radius is exactly the named set — never the whole artifact
   by default.
2. **The unnamed remainder may land** — provided it does not depend on a
   blocked section for its meaning.
3. **The dependency closure is author-declared and contestable.** The
   author publishes the dependency declaration ("section 5 does not
   depend on blocked section 3"); the reviewer may formally contest any
   edge of it; the contest and its resolution are recorded in the
   disposition. The declaration is a first-class review object —
   adversarially testable, not an informal assurance.

**The artifact state model (added after external review — both external
reviewers independently required it).** Under a standing scoped
rejection, "the artifact" is defined: every section carries exactly one
state from {UNREVIEWED, LANDED, BLOCKED, CONTESTED} — UNREVIEWED is the
birth state of every section, and nothing lands from it without a
verdict; the current certified version IS the LANDED set; a landed section MAY NOT reference a non-landed section —
which makes the dependency closure load-bearing for integrity, not just
for bookkeeping: an under-declared dependency corrupts the landed state
itself, not merely the record. Cross-references into blocked territory
therefore block the referencing section too, by construction.

**Contest semantics, fail-closed.** A contested dependency edge COUNTS AS
A DEPENDENCY until adjudicated (fail-closed — contest freezes, it never
frees), and adjudication is a named role BOUND AT REVIEW START (an identified
adjudicator, a declared contest timeout, and an escalation path: a
contest unresolved at timeout stays fail-closed AND escalates to the
artifact owner's choice — sustain the edge, strike it, or abort the
partial landing). Deadlock therefore has a defined exit that is not
silent whole-artifact blocking. This removes the reviewer's incentive
problem in one direction (contesting every edge merely restores
whole-artifact blocking, openly, attributably) and the author's in the
other (under-declaration is now an integrity defect with the author's
name on it, per the state model above).

Reference semantics, typed: only DEFINITIONAL dependence (a section's
meaning requires the blocked text) blocks; citation and historical
mention do not — the author types each cross-reference, and types are
contestable exactly like edges. Cyclic dependency groups land or block
as one unit. A later objection to an already-LANDED section opens a NEW
scoped review round against the landed set — prospective, never a
retroactive unlanding.

Failure modes, named: an author under-declares dependencies to land more
(now an integrity defect against the landed state, falsifiable and
attributable); a reviewer over-contests to restore whole-artifact
blocking (possible by design — but it is the fail-closed outcome made
visible and attributable, not a bypass).

## Rule register

| Part | State | Enforcement today |
|---|---|---|
| 1 — scoped REJECT | HARD (a verdict either names sections or does not) | procedural |
| 2 — remainder lands | HARD given an adjudicated closure; degrades to HEURISTIC while any relevant edge is CONTESTED | procedural |
| 3 — contestable closure | HEURISTIC (contest adjudication is judgment) | procedural |

## What this is NOT

Not a severity taxonomy (blocking vs non-blocking comments exist
everywhere; this scopes the BLOCKING itself). Not path-scoped approval
(CODEOWNERS scopes who must approve, not what a rejection freezes). Not a
merge-queue optimization — it is a semantics for partial landing under
standing objection, applicable to documents and policies as much as code.

## Relation to prior art (acknowledged, by name)

Line-item veto (scoped rejection with landing remainder, in law);
parliamentary division of the question (severable parts voted
separately); stacked-change review systems (Gerrit relation chains /
Depends-On: author-declared, discussion-contestable dependency graphs at
change granularity, with partial stack landing — the closest software
precedent, operating on commit topology rather than in-artifact semantic
dependency); IESG DISCUSS criteria (named-issue objections; whole-
document hold; contestable admissibility of the objection itself);
scoped review assignment practice (reviewers covering designated files
or aspects and noting coverage — cited as practice, without attributing
exact wording to any one guide); per-file review marks (Gerrit);
justified-veto conventions (Apache voting); clause-level dispositions in
standards recirculation (scopes RE-REVIEW, not rejection); W3C at-risk
feature removal in Candidate Recommendations; suggestion-mode
accept/reject in document editors — distinguished on substance, not
waved away: a suggestion is a PENDING PATCH, and rejecting it leaves the
certified text untouched; this mechanism scopes verdicts over EXISTING
certified content, which is why partial landing needs the state model
above and suggestion-mode does not.

## Enforcement maturity (self-disclosure)

Procedural everywhere. The mechanism is three data structures away from
platform enforcement (finding→section binding; a dependency-declaration
field; a contest record), and no platform ships them today. Nothing here
enforces honest dependency declarations beyond their recorded
falsifiability.

## Possible relations (not asserted)

This surface emerged from one operating practice in parallel with other
candidate surfaces: lineage-aware-agent-governance,
lineage-admission-control, disclosure-order-review,
falsifiability-first-protocol, claim-strength-profile. Common origin is asserted as a fact of production history; no relation
BEYOND common origin is asserted, and none is confirmed. Composition, dependency, or a unified
framework among any of them is possible and deliberately NOT asserted;
no confirmed relation exists, and none should be inferred from
co-ownership, shared vocabulary, or structural resemblance. Read under a
weakest-compatible-relation default: navigation adjacency. If a
composition is ever established it will be stated explicitly; absence of
that statement means it has not been.

## Public / internal boundary

No operational records or internal review histories appear here.
Non-inference runs both ways.

## Fork / derivative boundary

Source provenance is not inherited authority; attribution is not
endorsement; derivative decisions are not attributable upstream.

## Review questions (refutation invited)

1. Name a public review system doing this WITHIN one artifact, at
   section granularity, over semantic dependencies (the body already
   concedes veto/parliamentary/stacked-change forms). That defeats the
   re-scoped composite.
2. Name one requiring an author-declared, reviewer-contestable dependency
   map. That defeats part 3.
3. Is part 3 decidable in practice — do real contests over semantic
   dependency converge, or do they reproduce whole-artifact blocking by
   another name?
4. Does partial landing under standing objection create version-state
   ambiguity (what exactly is "the artifact" while section 3 is blocked)?
   Propose the state model or show the ambiguity is fatal.
5. Decomposition into per-section micro-artifacts under ordinary review
   is the standing simpler alternative. The answer this document gives:
   decomposition prices granularity at AUTHORING time and externalizes
   the dependency problem into unmanaged inter-artifact references with
   no contest mechanism; scoped rejection prices granularity at REVIEW
   time and keeps the dependency claims inside one governed object whose
   cross-section coherence is the artifact's value. Refute that answer,
   or produce a simpler structure with equivalent assurance — either is
   a successful challenge.

Negative findings are relevant findings.
