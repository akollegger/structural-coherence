# RFC-002 — The Semantic Layer as Restored Dampening: A Test of the Resonance Framework on Text-to-SQL

**Author:** Andreas Kollegger
**Affiliation:** Neo4j
**Status:** Experimental protocol — pre-registration draft; no results yet
**Version:** v3 (2026-07-05)
**Depends on:** RFC-001 (*Resonance: A Descriptive Account of How Latent Structure Keeps Growing Information Coherent*), §8.7

---

## Status of this document

This is the first experiment specified in full under the RFC-001 program. It is a pre-registration: it states a prediction derived from the Resonance framework, a protocol designed to confirm or falsify that prediction, and the operational definitions the framework-level draft deliberately left open. No data has been collected. The prediction is stated as firmly as the framework implies precisely so that a null or contrary result is meaningful; the experiment is designed to be able to disconfirm the framework's account, not only to corroborate it.

Where RFC-001 is a statics of a single store, this RFC tests one of its concrete claims in a setting — analytical databases queried in natural language — where a large, independently-published literature already exists to anchor and constrain the design.

---

## 1. What this experiment tests

RFC-001 makes a specific, falsifiable claim about relational databases (§8.7). Restated:

- A **denormalized schema** is a corpus that has deliberately traded dampening ($\sigma$) for read performance. Normalization enforces domain coherence by construction — each fact stored once, related facts reachable by declared joins over a typed vocabulary. Denormalization flattens that: it duplicates facts across wide tables, drops the relational constraints, and severs the column names and join paths from the domain meaning they encoded. In the framework's terms, denormalization is a **projection that discards the dimension along which the data was coherent** (RFC-001 §4.2.1), lowering $\sigma$ at the physical layer in exchange for avoiding join cost at read time.

- A **semantic layer** over that schema is **a priori compound structure at the seam** between the natural-language query and the physical model. It *dampens* — by re-declaring the canonical entities, measures, relationships, and disambiguation rules the denormalized model lost, restoring the domain coherence — and it *enriches* — by mapping a query onto derivable join paths and computed measures present in no single physical table. It is the composition/seam mechanism of RFC-001's Future Work appearing as a concrete artifact.

- The framework therefore predicts that natural-language-to-SQL degrades on denormalized schemas **because** the model is being asked to reconstruct load-bearing domain structure the schema projected away, and that a semantic layer helps **because** it restores that structure — not merely because it supplies better labels.

The existing literature (Section 2) has already established, robustly, that semantic layers help. What it has **not** isolated is the framework's specific mechanistic claim: that the benefit is *restored structural coherence* and that it *scales with how much coherence was lost*. That is what this experiment is designed to test, and — importantly — to be capable of falsifying.

---

## 2. Prior art and what it leaves open

The semantic-layer/text-to-SQL literature is unusually mature and points in one direction, which both anchors this experiment and sharpens what remains to be shown.

**The effect is large, paired, and independently replicated.** Rumiantsau & Fokeev (2026, "Semantic Layers for Reliable LLM-Powered Data Analytics") run a strictly paired benchmark — same model, same harness, same judge, varying only the presence of a ~4 KB semantic-layer document — over the Contoso retail dataset in ClickHouse, and report +17 to +23 percentage-point accuracy gains across three frontier models, with the models statistically indistinguishable *within* each condition. The BIRD benchmark's "external knowledge evidence" produces a ~+20 pp gap for GPT-4; Sequeda et al. (2023) report 16.7% → 54.2% on an enterprise insurance schema when querying an ontology rather than raw SQL; Zargari Marandi et al. (2024) report +70 pp on pharmacovigilance queries with a business-context document; Ganz & Perigaud (2026, dbt Labs) report modeled-semantic-layer gains up to 84.1% → 100.0%.

**The literature already frames the effect as structural, not capability-driven** — the same claim RFC-001 makes in its own vocabulary. Rumiantsau & Fokeev interpret their result as "a structural result: explicit business semantics suppress the dominant class of text-to-SQL errors not by making the model more capable, but by changing what the model is being asked to do," and observe that a smaller model with semantic context beats a larger model without it. Sequeda et al. and Allemang & Sequeda (2024) report that ontology grounding *changes the kind of error the model makes* — eliminating hallucinated classes and properties, leaving only path errors — which is a qualitative signature of restored structure, not merely improved labeling.

**Two gaps remain, and they are exactly the framework's claims:**

1. **No dose-response against denormalization degree.** Every paired study varies the *presence* of the semantic layer. None varies the *degree of denormalization of the underlying schema* and asks whether the semantic layer's benefit scales with it. The framework predicts it must: the benefit is proportional to the coherence lost in the projection to physical, so a normalized schema should benefit little and a heavily denormalized one should benefit most. This is a monotonic prediction no existing study has tested, and one a flat result would falsify.

2. **No decomposition of the layer into its structural mechanisms.** The existing semantic-layer documents bundle several distinct mechanisms and vary only their aggregate presence. It is tempting to split them into "naming" versus "structure" and treat naming as the null, documentation-only condition — but that split is wrong, and getting it right is one of this RFC's contributions. **Naming is itself structural.** It is not the absence of structure against which structure is measured; it is the first rungs of the same ladder, spanning the same $\phi$/$\sigma$ decomposition the framework uses throughout. Concretely, schema naming carries structure at three escalating levels:

   - **Appropriate** — a name maps to a real domain term (`customer_id`, not `col_7`). This reduces the *interpretation* burden: the reader need not reconstruct what a column means. It is the weakest level, closest to annotation, and declares no relationships.
   - **Consistent** — the same domain concept is named identically everywhere (`customer_id` in every table, never `cust_id` here and `customer` there). Naming consistency *is dampening* ($\sigma$): an inconsistent name is a soft inconsistency in the schema itself — one referent projected into two tokens, the schema-level instance of the unindexed-disagreement case in RFC-001 §4.2.1. Consistent naming is the controlled-vocabulary mechanism of the paper's dampening-dominant quadrant, applied to the schema's own identifiers.
   - **Conventional** — internal naming conventions carry *derivable* structure ($\phi$): if table `A` exposes `a_id`, then encountering `a_id` in table `B` lets a reader *infer* a join path that was never explicitly declared. A held convention makes the join graph recoverable from identifiers alone. Conventional naming is latent a priori structure — enrichment distributed into the names, exactly as a type lets one derive what is inferable.

   So the semantic layer is not "documentation plus structure." It is a *stack of structural layers*, the lowest of which is naming discipline: appropriate names cut interpretation cost, consistent names dampen, conventional names enrich, and explicit declarations (relationships and measure formulas a convention cannot encode) sit on top. The prior art varies the whole stack at once; it has never isolated the rungs.

RFC-002's contribution is therefore not to re-demonstrate that semantic layers help — that is settled — but to test *why* they help against the framework's specific account, using two manipulations the literature has not run: a denormalization-degree sweep, and a decomposition of the semantic layer into the ladder of structural mechanisms above, naming included as structure rather than excluded as its absence.

---

## 3. Predictions

Stated so that each can fail.

**P1 — Dose-response.** Holding the domain, question set, model, and harness fixed, and varying only the degree of denormalization of the schema the model queries, first-shot text-to-SQL accuracy in the *no-semantic-layer* condition **declines monotonically** with denormalization degree. Equivalently: the more coherence the physical schema has shed, the worse raw text-to-SQL performs. *Falsified if* accuracy is flat or non-monotonic in denormalization degree.

**P2 — Benefit scales with lost coherence.** The accuracy *lift* provided by a full semantic layer **increases monotonically** with denormalization degree: near zero on a fully normalized schema (little coherence to restore), largest on a heavily denormalized one. *Falsified if* the lift is constant across denormalization degrees, or largest on the normalized schema.

**P3 — The structural layers of naming each buy accuracy, and compound.** Decomposing the semantic layer into the ladder of Section 2 — appropriate naming, then consistent naming, then conventional naming, then explicit declaration — each increment adds accuracy over the one below, because each supplies a *different* mechanism (interpretation relief, then dampening, then enrichment, then declaration). *Falsified if* the increments do not order as predicted, or if a level that adds a new mechanism (notably consistency, the dampening rung, or convention, the enrichment rung) adds no accuracy over the level below it.

**P4 — The enrichment rungs scale with denormalization; the interpretation rung does not.** The benefit of *conventional* naming and of *explicit declaration* — the rungs that restore derivable join structure the physical model dropped — increases monotonically with denormalization degree, because that is the structure denormalization sheds. The benefit of merely *appropriate* naming (interpretation relief) is roughly constant across denormalization degrees, because opaque column names are a per-column burden largely independent of how normalized the schema is. *Falsified if* appropriate naming alone reproduces the dose-response, or if the convention/declaration rungs show no scaling with denormalization.

P3 and P4 together are the load-bearing predictions and the ones that distinguish the framework from the null "documentation helps" account. P1 and P2 could be explained by "denormalized schemas are confusing and any help helps more when things are worse." P3 and P4 are what separate *restored structure* from *better labels* — while recognizing, per Section 2, that better labels are themselves structure at the lower rungs, so the contrast is between *kinds* of structural help and how each scales, not between structure and its absence.

**P5 — Volume dose-response.** Holding denormalization degree and everything else fixed and sweeping *schema volume* (table/column count) exponentially, first-shot accuracy in the schema-only condition **declines with volume**, and declines **superlinearly** in the sense that the decline is better fit by a power law in table count than by a linear trend. *Falsified if* accuracy is flat in schema volume, or if a linear fit is not improved upon by the framework's superlinear form across the sampled range.

**P6 — The composite predicts better than either axis (the interaction).** Because denormalization lowers table count while raising per-query conflict, neither schema volume nor denormalization degree alone should predict accuracy as well as the framework's *composite* effective-conflict-surface — schema volume feeding the $V$ term, denormalization feeding $\delta$, per RFC-001's $\beta = 1 + \delta - \gamma$. Concretely: a heavily denormalized small-table schema and a lightly denormalized large-table schema can present the model with comparable effective conflict surfaces despite very different table counts, and the framework predicts their accuracies track the composite, not the raw table count. *Falsified if* table count alone (or denormalization alone) predicts accuracy as well as the composite does — which would mean the two-exponent structure buys nothing here and the volume and coherence effects are simply separable.

P6 is the prediction most specific to RFC-001, because it is the one place this experiment tests the *interaction* the two-exponent bound asserts rather than either factor in isolation.

---

## 4. Design

### 4.1 Two axes: schema volume and denormalization degree

The experiment varies two things about the schema the model must query, because the framework's subject is coherence *under volume*, and denormalization degree alone does not vary volume. Normalizing splits a domain's data across more, narrower tables; denormalizing folds it into fewer, wider ones — the same information, differently partitioned. These are two directions from a common reference, not two fixed schemas, and it is worth stating the relationship precisely because it is easy to garble: the *most-normalized* version has the *most* tables, and the *most-denormalized* version has the *fewest*. Table count therefore falls as denormalization rises. That anti-correlation is not a nuisance to be eliminated; it is the substance of the framework's prediction here, and the two-axis design exists to hold the axes apart so their separate and joint effects can be read.

**Axis 1 — schema volume (table/column count).** The volume the *model's coherence-reconstruction task* scales with. A larger schema forces the model to hold more relationships in mind to link a query to the right tables and joins, and the number of plausible-but-wrong join paths grows faster than the table count itself, since each new table can join against the existing ones. This is the direct analogue of RFC-001's $V$ for this setting — the "corpus" whose coherence is at stake is the schema as the model must reconstruct it, not the row data (see the data-volume note below).

Schema volume is swept **exponentially, not linearly** — roughly $2, 4, 8, 16, 32, 64, 128$ tables — for a framework-internal reason, not merely by convention. RFC-001 claims the conflict surface grows superlinearly, as $V^{1+\delta}$; if that holds for schema volume, the interesting behavior (schema-linking difficulty, proliferation of wrong join paths) changes fastest in the upper range, and linearly-spaced points from 1 to 100 would oversample the flat low-volume region where everything works and undersample the regime where the predicted compounding bites. Recovering an exponent — which RFC-001 §8.1–8.3 say the experiments exist to do — requires points spread across orders of magnitude; a power law cannot be fit from points clustered in the flat region, nor can "power-law decline" be distinguished from "linear decline" or "a cliff at some threshold" without log-spaced sampling.

**Axis 2 — denormalization degree.** How much coherence the physical model has shed at a given volume. Generate a graded series of progressively denormalized versions of the *same data*:

- **D0 — Most normalized.** Third-normal-form schema with declared primary/foreign keys; the most tables. Full physical dampening; domain coherence present in the physical model.
- **D1 — Lightly denormalized.** Common dimensions folded into fact tables; some redundancy introduced; keys retained.
- **D2 — Moderately denormalized.** Star/snowflake collapsed toward wider tables; several hierarchies flattened; some keys dropped.
- **D3 — Most denormalized.** "Fat" tables joining facts with dimensions (the pattern Rumiantsau & Fokeev describe for self-service deployments); duplicated facts; opaque column names; few or no declared constraints; the fewest tables.

**The two axes are crossed.** The grid of (schema volume × denormalization degree) is what makes this a test of RFC-001's central claim rather than of either factor alone. The framework's specific prediction is about their *interaction*: a denormalized schema has fewer tables (lower nominal schema volume) yet a higher per-query conflict surface (lost dampening), so accuracy should be predicted not by table count alone nor by denormalization alone but by the framework's composite — the *effective* conflict surface the model must reconstruct, in which schema volume feeds the $V$ term and denormalization feeds $\delta$. This mirrors RFC-001's $\beta = 1 + \delta - \gamma$ directly, and it is the version of the experiment that most nearly measures the quantity the framework is actually about.

Holding the *underlying answerable questions constant* is straightforward along the denormalization axis — the same data, differently partitioned, has the same ground-truth answers — but is genuinely hard along the volume axis, where more tables usually means more information and therefore a different set of askable questions. The design must either fix the domain's information content and vary only how it is partitioned (which normalization/denormalization does naturally, but a pure table-count increase does not), or accept that the volume axis samples related domains of increasing size and control for that statistically. This tension is real and is named again as a validity threat in Section 6.

**A note on data volume.** Row count is deliberately *not* an axis. Text-to-SQL accuracy is a function of the schema the model reasons over, not of how many rows the tables hold; the model writes SQL against structure, not data. We predict data-row volume has no effect on first-shot accuracy and hold it fixed, noting the exclusion here to preempt the natural question.

**A denormalization-degree metric must be committed in advance** (one of the operational definitions RFC-001 left open). Candidate: a composite of (i) redundancy — mean number of physical locations a given domain fact appears in; (ii) constraint loss — fraction of the most-normalized schema's declared keys/constraints absent in this version; (iii) name opacity — fraction of columns whose names no longer map to a domain term without the semantic layer. Combined into a single ordinal degree for the monotonicity tests and reported separately for diagnosis, pre-registered here rather than chosen after seeing results. Schema volume, being a table/column count, needs no such construction, but the specific volume rungs and how the same domain is scaled to hit them are pre-registered alongside it.

### 4.2 The semantic-layer conditions: a ladder of structural mechanisms

At each denormalization level, the model is evaluated under a cumulative ladder of context conditions, each adding one structural mechanism to the one below. The ladder is cumulative rather than a set of independent variants, because the framework's claim is about the *marginal* contribution of each mechanism, which is only meaningful as an increment over the mechanisms beneath it.

- **C0 — Schema only, opaque.** Raw DDL with the denormalized schema's actual (often opaque) identifiers, single-shot. The baseline (Rumiantsau & Fokeev's "raw" condition).
- **C1 — Appropriate naming.** Identifiers renamed to map to real domain terms, and annotated, but with no guarantee of cross-table consistency and no declared relationships. Isolates *interpretation relief*.
- **C2 — Consistent naming.** C1 plus the guarantee that each domain concept is named identically across every table. Isolates the *dampening* rung: the same referent now has one token, not several.
- **C3 — Conventional naming.** C2 plus held internal naming conventions (e.g. `a_id` as the key of table `A`, appearing as `a_id` wherever `A` is referenced) so that join paths become inferable from identifiers alone. Isolates the *enrichment* rung: derivable structure distributed into names.
- **C4 — Explicit declaration.** C3 plus the declarations a naming convention cannot encode — canonical entities, relationship semantics, measure formulas, disambiguation rules. The full semantic layer, comparable to the prior-art document.

Each rung adds exactly one mechanism, so the marginal accuracy from C(n) to C(n+1) attributes to that mechanism. The critical measurements are the *consistency* increment (C1→C2, the dampening rung) and the *convention* increment (C2→C3, the enrichment rung): these are the ones the framework predicts will (a) each add accuracy and (b) scale with denormalization degree, whereas the *appropriate-naming* increment (C0→C1, interpretation relief) should add accuracy but not scale with denormalization.

Authoring these rungs so that each adds *only* its own mechanism is the central protocol challenge (Section 6): the C1 document must be appropriately-named but deliberately inconsistent, the C2 document consistent but conventionally arbitrary, and so on. Holding documentation *quality* (length, care, coverage) constant across rungs while varying only the structural mechanism present is what makes the increments interpretable.

### 4.3 Models

Follow the prior-art design: at least two frontier models spanning a capability/cost range, plus one from a different vendor, to test whether — as RFC-001 predicts and Rumiantsau & Fokeev observe — the effect is structural (consistent across models) rather than capability-driven. Reasoning effort held constant across conditions. The framework predicts the *within-condition* model spread stays small while the *across-denormalization* and *across-rung* effects are large.

### 4.4 Grading

Paired, single-shot, execution-based grading against reference SQL, following Rumiantsau & Fokeev: execute reference and candidate against the same warehouse, judge row-level agreement, hold the judge constant across all conditions so any judge bias affects conditions equally. Report an analytical verdict (crediting benign reformulations) as primary and a strict verdict as a secondary check. Use a cross-family judge, or human adjudication on a sample, to address the judge-family confound the prior art flags as a limitation.

---

## 5. What each outcome would mean for RFC-001

The experiment is designed so that its outcomes bear on the framework, not just on text-to-SQL.

- **P1–P6 all hold:** the framework's account of denormalization-as-lost-dampening and the semantic layer as a stack of structural mechanisms is corroborated in a real setting, and — because §8.7 derives these from the same $\sigma$/$\phi$ decomposition and projection argument used throughout — this is evidence for the decomposition itself, not only for this application. In particular, the consistency rung behaving as dampening and the convention rung as enrichment is direct evidence for treating naming as structure spanning both, and P6's composite outperforming either axis is the closest this experiment comes to testing the two-exponent bound's interaction directly.
- **P1, P2 hold but P3/P4 fail** (the rungs do not order or scale as predicted — e.g. appropriate naming alone reproduces the dose-response): the framework's *direction* is right but its *mechanism* is mis-specified. If interpretation relief alone carries the effect, the semantic layer's benefit is not the restoration of derivable structure the framework claims, and §8.7's identification of the layer as *compound* (dampening + enrichment) structure would need revision toward an interpretation-cost account.
- **P2 fails** (lift constant or inverted across denormalization): the core claim that benefit scales with lost coherence is wrong, and §8.7 should be withdrawn or substantially rewritten. This is the cleanest single point of failure.
- **P1 fails** (raw accuracy flat across denormalization): the premise that denormalization sheds dampening in a way that degrades reconstruction is wrong, which would undercut the framework's treatment of denormalization as a $\sigma$-lowering projection.
- **P6 fails** (table count or denormalization alone predicts as well as the composite): the two-exponent structure buys nothing in this setting — volume and coherence act separably rather than combining into a single effective conflict surface. This would not refute the individual $\sigma$/$\phi$ claims but would undercut RFC-001's central move of folding both into one governing quantity $\beta$, at least for schemas; the framework would survive as two separate effects rather than one composite law.
- **P5 fails** (accuracy flat in schema volume, or no superlinearity): the claim that the model's coherence-reconstruction task scales with schema volume is wrong for this setting, suggesting text-to-SQL difficulty is not volume-driven in the way RFC-001's $V$-scaling assumes — a boundary on where the framework's volume dynamics apply.

Per the RFC-001 Status note, any of these outcomes is an acceptable result of the program: the framework is a specification to be fixed or scrapped against evidence, and this RFC is one place that adjudication happens.

---

## 6. Threats to validity

- **Isolating one mechanism per rung (the central threat).** Each rung must add *only* its own mechanism at constant documentation quality. If, say, the consistent-naming document (C2) is also inadvertently more careful or better-covered than the appropriate-naming one (C1), the consistency increment will absorb credit that belongs to quality, not dampening. Mitigation: author all rungs from a single shared term inventory; hold length, coverage, and care constant across rungs, varying only the target mechanism (consistency of tokens, presence of a held convention, presence of explicit declarations); and have a blind rater confirm the rungs differ *only* in the intended mechanism before the run. Authoring the deliberately-inconsistent-but-appropriate (C1) and conventionally-arbitrary-but-consistent (C2) documents is genuinely awkward and is the part of the protocol most likely to introduce artifacts; it should be treated as a gate on the experiment rather than an afterthought.
- **Constructed denormalization vs. natural denormalization.** A synthetically denormalized schema may not resemble the messy, organically-denormalized warehouses of practice. Mitigation: derive the sweep from a real denormalized warehouse where possible, normalizing *backward* to construct D0–D2 from an existing D3, rather than only denormalizing forward from a clean D0.
- **Constant information content across the volume axis (the threat specific to Axis 1).** Sweeping schema volume by table count risks confounding *volume* with *information content*: a 128-table schema usually answers more questions than a 4-table one, so a raw accuracy decline could reflect harder questions rather than more schema to reconstruct. Denormalization does not have this problem (same data, differently partitioned), but a pure table-count increase does. Mitigation: prefer scaling that holds the answerable-question set fixed while varying only how the domain is partitioned into tables (e.g. progressively splitting a fixed domain into more normal forms, or composing the domain from modular sub-schemas that add tables without adding new askable facts); where that is not fully achievable, hold the question set fixed to the facts answerable at the *smallest* volume and control statistically for residual differences. Name this in the pre-registration rather than discovering it in analysis.
- **Question-set sensitivity.** The effect concentrates in specific query classes (multi-fact-table disambiguation, snapshot-vs-flow, calculated metrics, sentinel keys, time anchoring — per Rumiantsau & Fokeev's error analysis). The question set must span these deliberately and report per-class results, or a dose-response could be an artifact of class mix shifting across schema versions.
- **Judge family bias.** As the prior art notes; addressed by a cross-family or human-audited judge on a sample.
- **Single domain.** Like the prior art, a single-domain result is an existence proof of the mechanism, not proof of domain-neutrality. RFC-001 §9 already declines the domain-neutrality claim; this RFC inherits that limitation and does not overreach it.

---

## 7. Relationship to the RFC-001 program

This experiment is the concrete, near-term instance of two RFC-001 threads: §8.7 (its home) and the composition/seam mechanism sketched in Future Work (§10), of which the semantic layer is a worked example — structure at the interface between intent and store. It does **not** test the flagship agentic-memory horizon experiment (§8.6), the two-exponent bound directly (§8.1–8.3), or the coherence-under-composition theorem; those remain for later RFCs. Its scope is deliberately one falsifiable mechanistic claim, chosen first because the prior-art base is strong enough that the experiment can be built on established benchmarks and grading methodology rather than from scratch.

---

## Version History

- **v3 (2026-07-05)** — Added the missing sense of *volume*. Introduced schema volume (table/column count) as a second axis, swept exponentially (~2–128 tables) rather than linearly, with the framework-internal rationale that fitting a superlinear conflict-surface exponent requires log-spaced points. Crossed it with the denormalization axis and added the interaction predictions P5 (volume dose-response, superlinear) and P6 (the composite effective-conflict-surface predicts better than table count or denormalization alone — the one place the two-exponent bound's interaction is tested directly). Corrected the normalize/denormalize language throughout (most-normalized = most tables; most-denormalized = fewest), noted the table-count/denormalization anti-correlation as substance rather than nuisance, excluded data-row volume as a non-factor, and added the constant-information-content-across-volume validity threat.
- **v2 (2026-07-05)** — Reframed the naming/structure ablation after recognizing that *naming is itself structural*. Replaced the false naming-vs-structure dichotomy with a taxonomy of naming as structure at three levels — appropriate (interpretation relief), consistent (dampening, $\sigma$), conventional (enrichment, $\phi$) — and recast the semantic layer as a cumulative ladder of structural mechanisms (C0 opaque → C1 appropriate → C2 consistent → C3 conventional → C4 explicit declaration). Split the old P3 into P3 (each rung adds accuracy and the increments compound) and P4 (the enrichment rungs scale with denormalization while the interpretation rung does not); updated the outcome mapping, the central validity threat, and the analysis plan accordingly.
- **v1 (2026-07-05)** — Initial protocol. Denormalization-degree sweep (D0–D3), four context conditions (schema / naming-only / structure-only / full) isolating naming from structure, three predictions (P1 dose-response in raw accuracy, P2 lift scales with lost coherence, P3 structure not naming carries the scaling), grounded in the 2023–2026 semantic-layer/text-to-SQL literature (notably Rumiantsau & Fokeev 2026, BIRD, Sequeda et al. 2023, Ganz & Perigaud 2026).

---

## References

- Allemang, D., & Sequeda, J. (2024). Increasing the LLM accuracy for question answering: Ontologies to the rescue! *ISWC 2024*, LNCS 15233. arXiv:2405.11706. *(Ontology grounding changes the class of error the model makes — a structural signature.)*
- Ganz, S., & Perigaud, P. (2026). Semantic Layer vs. Text-to-SQL: 2026 Benchmark Update. *dbt Developer Blog.* *(Paired modeled-semantic-layer benchmark on the ACME Insurance suite.)*
- Li, J., Hui, B., Qu, G., et al. (2023). Can LLM already serve as a database interface? A BIg Bench for large-scale database grounded text-to-SQLs (BIRD). *NeurIPS 2023.* arXiv:2305.03111. *(External-knowledge-evidence gap of ~+20 pp.)*
- Rumiantsau, M., & Fokeev, I. (2026). Semantic Layers for Reliable LLM-Powered Data Analytics: A Paired Benchmark of Accuracy and Hallucination Across Three Frontier Models. arXiv:2604.25149. *(Primary methodological anchor: paired design, structural-not-capability interpretation, error taxonomy, ClickHouse/Contoso harness.)*
- Sequeda, J., Allemang, D., & Jacob, B. (2023). A benchmark to understand the role of knowledge graphs on large language model's accuracy for question answering on enterprise SQL databases. arXiv:2311.07509. *(16.7% → 54.2% via ontology; enterprise-schema evidence.)*
- Shen, J., Wan, C., Qiao, R., et al. (2025). A study of in-context-learning-based text-to-SQL errors. arXiv:2501.09310. *(Error taxonomy; schema linking as >80% of failures — used to define the per-class question mix.)*
- Zargari Marandi, R., et al. (2024). Automating pharmacovigilance evidence generation: Using LLMs to produce context-aware SQL. *JAMIA Open.* arXiv:2406.10690. *(+70 pp with a business-context document; note that schema narrowing alone reached only 50%.)*

*[PLACEHOLDER — to add once the run is designed in detail: the specific domain and source warehouse for the denormalization sweep; the schema-volume rungs and the method for scaling the domain to hit them while holding answerable questions fixed; the committed denormalization-degree metric weights; the per-class question inventory; model versions and effort settings; judge configuration and the human-audit sampling plan; and the pre-registered analysis (monotonicity tests across denormalization degree, volume, and rungs; the power-law-vs-linear fit for P5; the composite-vs-single-axis model comparison for P6; paired McNemar structure; the per-rung marginal-lift contrasts for P3; and the rung-by-denormalization interaction for P4).]*
