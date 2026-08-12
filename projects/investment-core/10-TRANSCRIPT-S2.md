# PROBLEM — SESSION 2 (revised brief)

## Context: this is a re-run, with three changes

Session 1 ran 9 members and produced a single consensus option (`parallel-shadow`) plus a
control specification. The Principal has corrected the assignment. Session 2 changes:

1. **All 18 council members participate**, not 9.
2. **The deliverable is NOT one consensus decision.** It is an **ordered execution sequence** —
   a numbered queue: rule 1, rule 2, rule 3…; agent 1, agent 2, agent 3…; task 1, task 2, task 3…
   Things that get built and enforced **one after another, in order**, each with a gate that must
   be true before the next begins. The council's job is to establish **priority order**, not to
   pick a winner. Voting in Round 3 is therefore a **ranked ballot**, aggregated by Borda count.
3. **A material new fact about incentives has been supplied** (see below). It closes an open
   question from Session 1 and it is not favorable.

Session 1's evidence pack, verdict and transcript remain valid input. Do not redo that research.
Do not re-litigate `parallel-shadow` — it is settled. Sequence the work inside it.

---

## The original problem (unchanged)

A private investor ("the Principal") wants a multi-agent AI system for investment decision support.

- **Instruments:** US-listed equities, ETFs, bonds, gold.
- **Brokers:** Freedom24 (Cyprus, CySEC), Freedom Finance Armenia, a Polish bank brokerage.
- **Team of four:** Dmytro (head of direction) + analyst-traders Dima, Ruslan, Volodymyr.
- **Prime directive, stated by the Principal:** preserve capital first, compound second.
- **Asked for:** (a) mission, values, goal hierarchy grounded in documented mechanisms of Dalio,
  Buffett/Munger and others; (b) agent architecture — who owns what, evidence obligations,
  information exchange, disagreement resolution, human decision rights, what is never delegated;
  (c) a control system making "preserve first" measurable and enforceable, with kill-criteria.

---

## NEW FACT — Dmytro's compensation structure

**Dmytro receives a percentage of the quarterly result — of capital growth, counting all trades,
both positive and negative, as a total sum.**

This resolves Session 1 Unresolved Question #6, where Machiavelli explicitly flagged: *"if the head
of direction's compensation is already tied to drawdown-adjusted metrics rather than raw return,
much of this tension dissolves — that fact isn't in the evidence pack."*

It does not dissolve. It is raw quarterly return.

**Coordinator's structural reading, offered as evidence to be challenged, not as a finding:**
- A percentage of gains with no share of losses is an **option-like payoff**. Option value rises
  with volatility, so the rational incentive of the holder is to **increase portfolio variance**.
- **Quarterly measurement against a multi-year compounding objective is a horizon mismatch.**
  Variance drain (`g = μ − σ²/2`) reduces the Principal's terminal capital but does not reduce a
  quarterly gain-share.
- Session 1 built its entire governance layer on the *inference* that no one is paid to trigger a
  stop. That inference is now **confirmed and stronger than assumed**: the person best positioned
  to override a preservation rule is paid, quarterly, on the metric that overriding it improves.

**Three sub-facts NOT supplied, which materially change the magnitude — flag, do not assume:**
- Is there a **high-water mark** (must a prior negative quarter be recovered before a gain-share is
  paid)? Without one, −20% then +20% pays a bonus on the +20% while the Principal is still down.
- Is there any **clawback** for negative quarters?
- Is the growth measured on **realized trades or mark-to-market**?

---

## Session 1 conclusions carried forward as settled

- **Mode `parallel-shadow`**: deterministic control/exposure layer and analysis agents are built
  simultaneously; agents hold zero capital and zero execution authority until they beat a measured
  baseline. Unanimous, 9.25/9.5 against a 6.333 threshold, 5 DEALBREAKER positions.
- **Loss is defined as permanent impairment or forced sale — not drawdown.** No portfolio-level
  stop-loss. Drawdown gates new positions; it never forces selling.
- **Freedom24 + Freedom Finance Armenia are ONE counterparty**, not two — same parent (FRHC),
  which received an SEC Wells Notice in March 2026, unresolved as of Aug 2026. Limits are computed
  by ultimate parent. *(Primary SEC filing was egress-blocked; verify directly.)*
- **Compensation ceilings:** Freedom24/CySEC €20,000 · Poland/KDPW €22,000 · **Armenia: no
  securities-investor scheme identified** (negative search finding, needs CBA confirmation).
- **Freedom24 ships an official Tradernet MCP server for Claude Code that can place live orders.**
  No agent process may ever hold an order-placement credential.
- **Governed vs accepted:** the system governs custody concentration, leverage, position size,
  credential scope, cash floor, evidence requirements, the log. It accepts returns, correlation
  regimes, drawdown depth, market timing.

### Session 1 open items the sequence must absorb
- **θ (parent-group exposure cap) was never agreed.** Taleb: remove a leg, do not size it.
  Kahneman/Aurelius: cap by ultimate parent, tighter than the single-broker cap. Unresolved.
- **Who may amend the invariants** was raised by Munger and never answered.
- **The re-entry path** (who may loosen a gate, and how) was flagged by Meadows as under-specified.
- **Agent scoring schema** was declared a precondition by Karpathy and never designed.
- **Unanimity across a single-provider council is itself a correlation risk**, flagged by Kahneman
  and by the Chairman.

---

## What Session 2 must produce

Three ordered queues, each item gated on the previous:

- **ORDER OF RULES** — which constraint is enforced first, second, third… Not all rules can ship at
  once; which one, if it alone existed, would prevent the most irreversible loss?
- **ORDER OF AGENTS** — which agent is built first, second, third… including deterministic
  components, and what each must prove before the next is built.
- **ORDER OF TASKS** — the actual execution queue for the humans and the developers.

Ordering is the deliverable. A brilliant rule in position 7 that should be in position 1 is a
defect. Sequence beats completeness.

---

# CANDIDATE POOL — items to be ordered

Rank these by ID. You may ADD items (give them a new ID with your initial, e.g. `R-NEW-x`) and you
may argue an item should be DELETED. But rank using these IDs so ballots can be aggregated
mechanically across 18 members.

## RULES — candidate constraints

| ID | Rule |
|---|---|
| `R-CRED` | No process in the agent runtime holds a broker credential with order-placement scope. Boot-time refusal, code-enforced |
| `R-PARENT` | Exposure limits computed by **ultimate parent group**, not by broker name (Freedom24 + Freedom Armenia = one counterparty) |
| `R-LEVER` | Zero leverage, zero margin, zero derivatives |
| `R-SIZE` | Position size ≤ ½ Kelly on a conservative edge estimate; ≤1% of equity at risk per position, volatility-scaled |
| `R-SOURCE` | Every number carries `source_url` + `retrieved_at`; unsourced values rejected by schema, not by review |
| `R-OVERRIDE` | Any override requires dual sign-off (never Dmytro alone) + simultaneous out-of-band escalation direct to the Principal |
| `R-AMEND` | Only the Principal amends thresholds; cooling-off delay; immutably logged (the meta-invariant) |
| `R-PHASE` | PRESERVE→COMPOUND gate opens on evidence, never on elapsed calendar time |
| `R-NOSTOP` | No portfolio stop-loss. Drawdown blocks new positions; it never forces a sale |
| `R-CASH` | Cash floor in short-duration high-quality paper |
| `R-SILENCE` | A month with zero flagged agent disagreements is a failure signal, not harmony |
| `R-EXIT` | Reduce or exit one Freedom-group leg |
| `R-COMP` | Restructure Dmytro's compensation so it is not a quarterly gain-share on raw return |

## AGENTS / COMPONENTS — candidate build order

| ID | Component |
|---|---|
| `A-LEDGER` | Deterministic ledger: positions and cash across three brokers, read-only ingestion |
| `A-PARENT` | Counterparty aggregation by ultimate parent + compensation-ceiling map |
| `A-GATE` | Gate function `G(state, proposal) → {accept, reject, escalate}` + invariants I1–I8 |
| `A-CHRONICLER` | Immutable append-only log: inputs, prompts, model versions, sources, human decisions |
| `A-OVERLAP` | ETF holdings-overlap computation (weight intersection, in-house) |
| `A-DURATION` | Bond duration/convexity sensitivity (QuantLib) |
| `A-SCORER` | Forecast registry and scoring harness: probabilistic schema, resolution dates, baseline |
| `A-RISK` | Risk analyst: sizing, `N_eff`, stress scenarios, counterparty exposure |
| `A-ETF` | ETF analyst: TER, AUM, liquidity, replication method, sec-lending, counterparty |
| `A-EQUITY` | Equity analyst: owner earnings ranges, debt, competence boundary, falsifiers |
| `A-MACRO` | Macro/regime: "where do we stand" from observables, never forecasts |
| `A-STRATEGY` | Strategy synthesis: proposals in the format `G` accepts |
| `A-DEVIL` | Devil's advocate — adversarial, on a different model or provider |

## TASKS — candidate execution queue

| ID | Task |
|---|---|
| `T-LEDGER` | Dmytro produces the Counterparty & Credential Exposure Ledger (real NAV split, real key scopes from the broker) |
| `T-LEVER` | Establish whether leverage, margin, or any forced-sale obligation currently exists |
| `T-KEYS` | Rotate all broker credentials to read-only; trade-scoped keys moved outside the agent runtime |
| `T-VERIFY` | Verify the two egress-blocked facts: FRHC 8-K/Wells response on EDGAR; Armenian securities-investor scheme with the CBA |
| `T-COMP` | Principal restructures Dmytro's compensation; clarify high-water mark, clawback, realized vs mark-to-market |
| `T-THETA` | Principal sets θ and resolves the Taleb-vs-majority split (exit a leg vs cap the group) |
| `T-ENGINE` | Build the deterministic ledger + exposure engine + daily report |
| `T-GATE` | Build `G` and invariants, with boot-time credential refusal |
| `T-SCORING` | Pre-register the agent scoring schema (format, resolution dates, baseline, sample size) |
| `T-AGENTS` | Build shadow analysis agents |
| `T-AMEND` | Design the amendment and re-entry path: who may loosen a gate, quorum, cooling-off |
| `T-REVIEW` | Graduation review: do the agents beat the baseline |
| `T-INDEP` | Obtain an independent cross-provider or human-specialist review of the two load-bearing claims |

---

# SESSION 2 — ROUND 1 ORDERINGS (18 members, identities masked)

One of these is yours. Evaluate by argument quality. Refer to peers only as "Member X".

---

**Member A** — *Principle:* irreversibility per unit of cost; what closes an absorbing barrier first, what improves an average last. A rule safe only under an unverified condition must follow the verification.
RULES: 1 `R-CRED` · 2 `R-LEVER` (the condition under which every settled rule is safe — must be *verified*) · 3 `R-COMP` (an option payoff on quarterly raw return manufactures variance daily and costs one signature to remove — delete the incentive before building governance against it) · 4 `R-OVERRIDE` · 5 `R-PARENT` · 6 `R-AMEND` · 7 `R-NOSTOP` · 8 `R-SIZE` · 9 `R-EXIT` (gated on ledger: exiting an 8%-of-NAV leg is theatre) · 10 **new `R-NEW-T`: no middle — every position is safe-leg or capped-convex; the mismeasured middle is rejected.** Wave 2: `R-CASH`, `R-SOURCE`, `R-PHASE`, `R-SILENCE`.
AGENTS: `A-LEDGER` → `A-PARENT` → `A-GATE` → `A-OVERLAP` → `A-CHRONICLER` (must precede the first LLM token) → `A-SCORER` → `A-RISK`+`A-DEVIL` same wave, different provider ("no devil, no risk agent"). Last: `A-STRATEGY` (most resembles authority).
TASKS: `T-KEYS` → `T-LEVER` → `T-LEDGER` → `T-COMP` → `T-VERIFY` → `T-INDEP` → `T-THETA` → `T-ENGINE` → `T-GATE` → `T-AMEND` → `T-SCORING` → `T-AGENTS` → `T-REVIEW`.
*Comp:* promotes `R-COMP` above every measurement task. Also makes my own `R-NOSTOP` more dangerous — no stop plus a variance-seeking overrider is the one combination never stress-tested.
*Weakness:* magnitude unsupplied (HWM, clawback, realized vs MTM); if the share is trivial I have over-promoted it.

**Member B** — *Principle:* first what forecloses the most guaranteed-failure paths at near-zero cost, and what stops later items depending on trusting the actor the new fact says cannot be trusted.
RULES: 1 `R-CRED` · 2 `R-COMP` (must precede `R-OVERRIDE`: an override rule signed by someone paid on raw variance is theater) · 3 `R-PARENT` · 4 `R-AMEND` · 5 `R-OVERRIDE` · 6 mechanical batch · 7 `R-EXIT`, `R-SILENCE`.
AGENTS: `A-LEDGER` → `A-CHRONICLER` (before anyone's output, including Dmytro's, is trusted) → `A-PARENT` → `A-GATE` → `A-SCORER` → analysts last.
TASKS: `T-KEYS` → `T-COMP` → `T-LEDGER` **but not from Dmytro alone** → rest.
*Comp:* **inverts the sequence.** `T-LEDGER` was assigned to the person now incentivized to understate concentration — concentration = variance = his upside. **New `R-NEW-M`: the exposure ledger requires independent verification before it gates θ.**
*Weakness:* may underweight Member E's formal dependency logic.

**Member C** — *Principle:* order by irreversibility during the build window, then by how much human judgment the rule requires. A rule executing in code precedes any rule depending on a person whose incentives oppose it. Measure before you threshold: a number set before the ledger exists is an anchor, not a limit.
RULES: 1 `R-CRED` · 2 `R-SOURCE` (or invented figures — like the "55%" in a prior pre-mortem — become anchors nobody can dislodge) · 3 `R-PARENT` (a definition, not a cap) · 4 `R-AMEND` (cheap written before thresholds exist; after, it is a fight with whoever benefits from the loose one) · 5 `R-OVERRIDE` · 6 `R-LEVER` · 7 `R-NOSTOP` · 8 `R-COMP` · 9–13 rest, `R-EXIT` last.
AGENTS: `A-LEDGER` → `A-CHRONICLER` → `A-PARENT` → `A-GATE` → `A-SCORER` → `A-DEVIL` cross-provider early and cheap → analysts.
TASKS: `T-LEDGER` → `T-KEYS` → `T-LEVER` → `T-COMP` → **`T-INDEP` at 5 (independent estimates *before* discussion; worthless after θ is set)** → `T-VERIFY` → `T-AMEND` → `T-THETA` → rest.
*Comp:* changes who holds the pen, not what is built first. **Availability bias will push this council to rank `R-COMP` first because it is the newest and most vivid fact; resist — magnitude is unknown until HWM, clawback and realized-vs-mark are answered. Ascertain, then restructure.**
*Weakness:* may be substituting "measure more" for "act". If the ledger shows a large FRHC share, `R-EXIT` should jump to position 2 and my ordering was wrong by six slots.

**Member D** — *Principle:* A precedes B when A closes a stock/flow that B's control logic silently assumes is already closed — otherwise B is a rule on paper while the loop routes around it.
RULES: 1 `R-CRED` · 2 `R-OVERRIDE` (the balancing loop directly targeting the reinforcing loop the comp fact confirms: option payoff → variance-seeking → solo override) · 3 `R-PARENT` · 4 `R-AMEND` · 5 `R-SIZE`/`R-LEVER` · 6 `R-SILENCE` later.
AGENTS: `A-LEDGER` → `A-PARENT` → `A-GATE` → `A-CHRONICLER` → `A-DEVIL` before the analyst pack scales (or you get ρ→1 agreement with no counterweight) → `A-SCORER`.
TASKS: `T-KEYS`+`T-LEDGER` parallel → `T-LEVER` → `T-VERIFY` → `T-THETA` → rest.
*Comp:* reorders, does not reweigh. `R-COMP` is highest-leverage in principle but has long negotiation delay, so it **cannot gate the first wave — that's a shifting-the-burden trap** where fast symptomatic relief substitutes for the structural fix and the fix never lands. Containment ships now; `T-COMP` starts in parallel today.
*Weakness:* may be over-ranking `R-OVERRIDE` above `R-PARENT`.

**Member E** — *Principle:* A precedes B iff A supplies a symbol B's predicate reads, or closes a precondition making B's guarantee formally valid.
RULES: 1 `R-CRED` · 2 `R-LEVER` (without it `R-NOSTOP`'s premise is false) · 3 `R-SOURCE` · 4 `R-AMEND` before `R-OVERRIDE` · 5 `R-OVERRIDE` · 6 `R-PARENT` (definable now, enforceable after `A-PARENT`) · 7 `R-SIZE` · 8 `R-PHASE`/`R-NOSTOP`/`R-CASH` · 9 `R-SILENCE` late by construction · 10 **`R-EXIT` and `R-COMP` are not rules — they are Principal decisions.**
AGENTS: `A-LEDGER` → `A-PARENT` → `A-CHRONICLER` (must log before `A-GATE` decides, or decisions are unauditable by construction) → `A-GATE` → `A-SCORER` (registry must predate any forecast it scores) → analysts → `A-STRATEGY` → `A-DEVIL` last by definition.
TASKS: `T-LEDGER` → `T-KEYS` → `T-LEVER` → `T-VERIFY` → `T-COMP` → `T-THETA` → `T-ENGINE` → `T-GATE` → `T-SCORING` → `T-AMEND` → `T-AGENTS` → `T-REVIEW` → `T-INDEP`.
*Comp:* moves `T-COMP` to 5 — no data dependency on the ledger, so it runs **parallel, not serial**. Formally: dual sign-off is necessary but insufficient if both signers share the same convex payoff.
*Weakness:* treats data-availability as the only ordering axis; may under-weight political urgency.

**Member F** — *Principle:* rank first whatever the Principal can impose **without needing the incentivized actor's consent**, since consent-dependent fixes stall.
RULES: 1 `R-OVERRIDE` · 2 `R-AMEND` (else override is defeated by redefining "override" instead of triggering it) · 3 `R-CRED` · 4 `R-PARENT` · 5–12 rest · **13 `R-COMP` — correct in principle, wrong to gate on: Dmytro has no incentive to volunteer it.**
AGENTS: `A-GATE` → `A-CHRONICLER` (the log he would need to reframe a breach as "context") → `A-LEDGER` → `A-PARENT` → `A-SCORER` → `A-RISK` → `A-DEVIL` → `A-STRATEGY` (the agent whose output a variance-seeking reader would selectively adopt — must never run ungated) → rest.
TASKS: `T-KEYS` → `T-LEDGER` → `T-LEVER` → `T-COMP` (parallel, non-blocking) → `T-VERIFY` → `T-THETA` → `T-GATE` → `T-ENGINE` → rest.
*Comp:* confirms rather than changes my order, but I underweighted that **Dmytro can stall `T-COMP` indefinitely — his option value is worth more unfixed.** Comp reform may never land on his terms.
*Weakness:* placing `A-DEVIL` before `A-STRATEGY` may be over-engineering before the boring engine ships.

**Member G** — *Principle:* A precedes B when B cannot be *measured* without A existing. Deterministic plumbing precedes anything you'd score; a scoring harness precedes anything you'd grade or trust.
RULES: 1 `R-CRED` · 2 `R-PARENT` · 3 `R-LEVER` · 4 `R-SOURCE` · 5 `R-SIZE`/`R-OVERRIDE`/`R-AMEND` · 6 `R-NOSTOP`/`R-CASH`/`R-PHASE` · 7 `R-SILENCE` undefined until agents exist.
AGENTS: deterministic substrate (`A-LEDGER`, `A-PARENT`, `A-GATE`, `A-CHRONICLER`) → **`A-SCORER` before any analysis agent writes a single forecast** → low-consequence analysts → `A-RISK`/`A-STRATEGY` → `A-DEVIL` last (needs a baseline consensus to attack).
TASKS: `T-LEDGER` → `T-KEYS` → `T-LEVER` → `T-VERIFY` → `T-COMP` → `T-THETA` → `T-ENGINE` → `T-GATE` → `T-SCORING` → `T-AMEND` → `T-AGENTS` → `T-REVIEW` → `T-INDEP`.
*Comp:* moves `T-COMP` ahead of `T-THETA`. He is structurally motivated to rush graduation — the metric his bonus rewards is the one the scoring schema exists to gate.
*Weakness:* I flagged scoring-as-precondition last round, so I am biased toward over-ranking it.

**Member H** — *Principle:* imagine each item absent tomorrow and ask whether the resulting loss can be undone.
RULES: 1 `R-CRED` · 2 `R-LEVER` (if leverage exists the whole verdict is void and everything below is ranked against the wrong world) · 3 `R-AMEND` **promoted above override** — a rule its own author may quietly loosen is not a rule · 4 `R-OVERRIDE` · 5 `R-PARENT` · 6 `R-NOSTOP` declared early and deliberately (the panic sale happens before the sophisticated rules ship) · 7 `R-SOURCE` · 8 `R-SIZE` · 9 `R-CASH` · 10 `R-COMP` (a Principal act, must precede any grant of authority).
AGENTS: `A-LEDGER` → `A-PARENT` → `A-CHRONICLER` (before the first decision under G, or the record begins with a gap) → `A-GATE` → `A-SCORER` → `A-DEVIL` before the analysts it must contest → rest, `A-STRATEGY` last.
TASKS: `T-LEDGER` → `T-KEYS` → `T-LEVER` → `T-VERIFY` → `T-COMP` → `T-THETA` → `T-AMEND` → `T-ENGINE` → `T-GATE` → `T-SCORING` → `T-INDEP` → `T-AGENTS` → `T-REVIEW`.
*Comp:* lifts `R-AMEND` above `R-OVERRIDE` and pulls `T-COMP` into wave one. **This is not a control problem but an authorship problem.** Fix the payoff or accept every rule below is paper.
*Weakness:* may be accepting the compensation structure as fixed when one could simply refuse to build until it changes.

**Member I** — *Principle:* X precedes Y iff X compiles and runs with zero external dependency and Y's correctness cannot be verified without X. Boring, testable, deletable code beats judgment.
RULES: 1 `R-CRED` (day 1) · 2 `R-LEVER` (one config check, day 1) · 3 `R-SOURCE` (day 1) · 4 `R-PARENT` · 5 `R-SIZE` · 6 `R-CASH` · 7 `R-OVERRIDE` (needs a gate to override) · 8 `R-AMEND` · 9 `R-PHASE`/`R-SILENCE` late · 10 **`R-EXIT`/`R-COMP` are not engineering — Principal decisions; they block on their own tasks, not on the build.**
AGENTS: `A-LEDGER` → `A-PARENT` → `A-CHRONICLER` → `A-GATE` → `A-SCORER` → `A-OVERLAP`/`A-DURATION` → shadow analysts → `A-STRATEGY`/`A-DEVIL` last.
TASKS: parallel week 1 — `T-LEDGER`, `T-KEYS`, `T-LEVER`, `T-VERIFY`. Parallel Principal track — `T-THETA`, `T-COMP`. Then `T-ENGINE` → `T-GATE` → `T-SCORING` → `T-AGENTS` → `T-REVIEW` → `T-AMEND`/`T-INDEP` last.
*Comp:* **no ordering change.** `R-OVERRIDE`/`R-AMEND` already assumed the overrider is compromised; this confirms it, doesn't move the build queue.
*Weakness:* may be under-ranking `A-CHRONICLER` — audit gaps compound silently.

**Member J** — *Principle:* order by *cause*: remove **efficient causes** of irreversible loss (who/what can act) before writing **formal causes** (rules), and know the **material** (actual facts) before setting any parameter.
RULES: 1 `R-CRED` · 2 **`R-COMP` — category error in the pool: this is not a system rule, it is a contract term, and it is the efficient cause of every override the other rules exist to resist. Fixing the source costs one document; compensating for it costs a governance layer forever.** · 3 `R-AMEND` · 4 `R-OVERRIDE` · 5 `R-LEVER` (a precondition, not a peer rule) · 6 `R-NOSTOP` (a definition — rank it, don't build it) · 7 `R-SOURCE` · 8 `R-PARENT`. Wait: `R-SIZE`, `R-CASH`, `R-EXIT`, `R-SILENCE`.
AGENTS: `A-LEDGER` (material cause) → `A-PARENT` (a *view*, not a system) → `A-CHRONICLER` **before the gate** → `A-GATE` → `A-OVERLAP`/`A-DURATION` (mis-genused as agents; ship with the engine) → `A-SCORER` → analysts.
TASKS: 1 `T-LEDGER`+`T-LEVER` (one interview, one day — separating them is artificial) · 2 `T-KEYS` · 3 `T-COMP` — **order by irreversibility × latency; this has the longest human latency** · 4 `T-VERIFY` · 5 `T-INDEP` · 6 `T-AMEND` · 7 `T-THETA` · rest.
*Comp:* changes the *genus*: the system is no longer guarding against error but against a paid-for behavior.
*Weakness:* over-classification. If FRHC is 8% of NAV my genus split is scaffolding around a rounding error.

**Member K** — *Principle:* enforce first what is decidable today with no unknown input and closes an irreversible channel; anything requiring a number nobody has is not a rule yet, it is a wish.
RULES: 1 `R-CRED` · 2 `R-AMEND` (a rule shipped before the amendment rule is amendable by whoever is paid to amend it — **and the Principal must accept being bound too**) · 3 `R-LEVER` · 4 `R-OVERRIDE` (governs the act, not the number; works before any threshold) · 5 `R-PARENT` aggregation only · 6 `R-SIZE` — enforce the ≤1% clause now, ½-Kelly is uncomputable until edge is measured · 7 `R-SOURCE`. **Delete `R-COMP` as a rule — it is a contract the system cannot enforce; it is `T-COMP`.**
AGENTS: `A-LEDGER` → `A-PARENT` → `A-CHRONICLER` (an unlogged gate cannot be shown to have been bypassed) → `A-GATE` → `A-SCORER` → **`A-DEVIL` before any analyst, so no analytic agent is ever unopposed** → rest, `A-STRATEGY` last.
TASKS: `T-KEYS` → `T-LEVER` → **`T-LEDGER` but broker-attested, not Dmytro-attested** → `T-COMP` → `T-INDEP` → `T-AMEND` → `T-THETA` → rest.
*Comp:* demotes `T-LEDGER` from first — Session 1 assigned the measuring document to the man the measurement governs. **And: if growth is realized-only, the payoff rewards never selling losers — which is exactly what `R-NOSTOP` permits.**
*Not yet:* **`R-NOSTOP` is a conclusion, not a rule** — it holds only if leverage is zero and no forced-sale obligation exists, never established. Ranking it first removes a protection before verifying its premise.
*Weakness:* decidability may privilege the easy over the important; `R-CRED` may be first because it is trivially first, not because it saves the most capital.

**Member L** — *Principle:* A precedes B when violating A produces harm with **no other fact needing to be true first** — what could go wrong today, with zero market movement required.
RULES: 1 `R-CRED` · 2 `R-PARENT` · 3 `R-OVERRIDE` · 4 `R-AMEND` · 5 `R-SIZE` · 6 the conditional batch · 7 `R-EXIT`/`R-COMP` political, gated on their tasks.
AGENTS: `A-LEDGER` ("poke it and see") → `A-PARENT` → `A-CHRONICLER` → `A-GATE` → `A-SCORER` → analysts last.
TASKS: `T-KEYS` → `T-LEDGER` → `T-LEVER` (**binary — if leverage exists the whole no-stop-loss architecture is false**) → `T-VERIFY` → `T-THETA` → `T-GATE`/`T-ENGINE` → `T-SCORING` → `T-AMEND` → `T-AGENTS` → `T-REVIEW` → `T-INDEP`. `T-COMP` parallel from day one.
*Comp:* doesn't reorder engineering — the rules already assumed nobody trustworthy by default. Moves `T-COMP` to start day one in parallel.
*Weakness:* may underweight how long comp negotiation actually takes relative to engineering — that could be the true bottleneck.

**Member M** — *Principle:* an adversary neutralizes what he can see coming. Build what removes his *capability* before what merely *measures* or *persuades* him — and **never signal a move against him while he still holds power to react first.**
RULES: 1 `R-CRED` · 2 `R-OVERRIDE` · 3 `R-PARENT` · 4 `R-AMEND` · 5 `R-COMP` — sequenced after 1–2, **but before he learns the credential lock is coming** · 6 `R-EXIT` **re-specified as a scheduled reduction, not a binary move** — exiting before the locks telegraphs distrust to the one person able to front-run it with a variance-maximizing quarter · 7 steady-state governance.
AGENTS: `A-LEDGER` → `A-PARENT` → `A-CHRONICLER` (what makes an override *dispute-proof* — the actual deterrent) → `A-GATE` → `A-DEVIL` before analysts → rest.
TASKS: `T-KEYS` **(rotate now, silently)** → `T-LEDGER` → `T-VERIFY` → `T-COMP` → `T-THETA` → rest.
*Comp:* confirms an adversary with rational cause, not a hostile one. **`T-KEYS` must land before `T-COMP` is discussed with him, or he has one quarter's warning to maximize variance.**
*Weakness:* may be over-treating him as adversarial when he is merely misaligned; silent rotation before disclosure carries an unpriced trust cost.

**Member N** — *Principle:* first, zero-dependency items closing the fastest irreversible action, or measurement preconditions. Everything else ordered by **when its risk actually arrives**, not by urgency of construction.
RULES: 1 `R-CRED` · 2 `R-PARENT` · 3 `R-OVERRIDE` (cheap immediate stopgap, because `R-COMP` is a negotiation with no fixed close date) · 4 `R-AMEND` · 5 **`R-COMP` — its deadline isn't "soon", it's *before the first live quarter-end*, when the option-like payoff bites** · 6 `R-LEVER`/`R-SIZE` · 7 `R-EXIT` after θ · 8 `R-SILENCE`.
AGENTS: `A-LEDGER` → `A-PARENT` → `A-GATE` → `A-CHRONICLER` → `A-SCORER` before `A-STRATEGY` → analyst wave → `A-DEVIL` last.
TASKS: `T-KEYS` ∥ `T-LEDGER` ∥ `T-LEVER` → `T-VERIFY` → `T-COMP` (deadline = first live quarter close) → `T-THETA` → rest.
*Comp:* moves it from background to **time-boxed**: quarterly measurement means the incentive recurs every 90 days.
*Weakness:* the quarter-end urgency is mechanistic inference; a high-water-mark clause would neutralize it entirely.

**Member O** — *Principle:* A precedes B when A removes a decision the *user* — the team at 7am under pressure — would otherwise have to make correctly by judgment. Fewest judgment calls first.
RULES: 1 `R-CRED` (zero judgment required) · 2 `R-PARENT` (one number per real counterparty, not three misleading ones) · 3 `R-LEVER` (absolute, unconfigurable — no threshold to tune, no dashboard to read) · 4 `R-AMEND` · 5 `R-OVERRIDE` (now load-bearing, not procedural). **`R-SILENCE` is a monitoring signal, not a gate — delete from rules, move to reporting. `R-EXIT`/`R-COMP` are Principal decisions and do not belong in this list at all.**
AGENTS: `A-LEDGER` → `A-PARENT` (without it the ledger lies by omission) → `A-GATE` → `A-CHRONICLER`. All analysis agents after: **a user with a perfect gate and no analysts is safe; a user with brilliant analysts and no gate is exposed.**
TASKS: `T-KEYS` → `T-LEDGER` → `T-LEVER` → `T-VERIFY` → `T-COMP` → `T-THETA` → `T-GATE` → `T-ENGINE` → rest.
*Comp:* the person who authors the ledger is the person paid on raw quarterly gain. **Not a sequencing detail — a user-trust defect. Someone else must verify the numbers.**
*Weakness:* may under-weight that `T-VERIFY` gates everything's *meaning*, not just order.

**Member P** — *Principle:* what removes an irreversible option ranks above what adds a control; what requires no build, no number and no agreement ranks above what requires all three. **Subtraction ships first because it cannot be gamed, delayed, or half-built.**
RULES: 1 `R-CRED` · 2 `R-LEVER` · 3 `R-NOSTOP` (a deletion, free, immediately true once 2 holds) · 4 `R-COMP` — **delete the distortion instead of building governance against it; `R-OVERRIDE`/`R-AMEND` are machinery bought to counteract exactly this** · 5 `R-PARENT` · 6 `R-EXIT` — if FRHC >25% NAV this becomes rule 1; **removing the leg deletes θ, `A-PARENT` and the ceiling map — one subtraction retires three builds** · 7 `R-SOURCE` · 8 `R-OVERRIDE` then `R-AMEND`, shipped with the gate.
**New `R-NEW-L1`: no rule ships until the previous one has been observed binding at least once; every rule and component sunsets in 12 months unless it has demonstrably bound something.**
**Defer/delete:** `R-SIZE` (½ Kelly on an unestimable edge is fake precision — Kelly is quadratic in σ), `R-CASH` (an added position with guaranteed real drag), `R-SILENCE`, `R-PHASE`.
AGENTS: `A-LEDGER` **hand-maintained one page first; automate only after a month of it surviving by hand** → `A-CHRONICLER` → `A-GATE` (`A-PARENT` folds into it, or dies with `R-EXIT`) → `A-SCORER` → **`A-DEVIL` first LLM built, different provider — if only one exists, make it the one that attacks** → `A-OVERLAP` → analysts. **`A-STRATEGY`: argue deletion — the four humans are the synthesis layer.**
TASKS: `T-KEYS` → `T-LEVER` (one question, one hour) → `T-LEDGER` → `T-COMP` (one signature; add HWM, clawback, realized-only) → `T-VERIFY` → `T-INDEP` (cheap, no build; **buy the dissent this council cannot generate**) → `T-THETA` → rest.
*Comp:* the correct response to a bad incentive is **removal, not surveillance**. Without a high-water mark the payoff is a free straddle; the three missing sub-facts are the actual deliverable of `T-COMP`.
*Not yet:* **thirty-nine new objects for a system diagnosed as over-structured is the previous fix generating the next problem.**
*Weakness:* low confidence on the deletions; if the portfolio is genuinely levered, `R-SIZE` outranks my ordering entirely.

**Member Q** — *Principle:* what can be changed by a signature precedes what must be built; what makes a later rule *believed* precedes the rule itself. **A constraint enforced before its owner has consented to it isn't a control — it's the rehearsal for the first override.**
RULES: 1 `R-CRED` · 2 `R-COMP` (a pen stroke, not a build; deletes the demand for half the governance layer) · 3 **new `R-NEW-W-CONSENT`: the Principal signs the "Acceptable Compromises" list *as a list of things he is giving up*. Until then rules 4+ are documentation.** · 4 `R-AMEND` (decide who may move a number *before* any number exists; afterwards it's a concession) · 5 `R-SOURCE` · 6 `R-LEVER` · 7 `R-NOSTOP` · 8 `R-PARENT` · 9 `R-OVERRIDE` · rest. **Delete `R-EXIT` from the rule queue — it is an outcome of θ; ranking it as a rule pre-decides the Session-1 split by smuggling.**
AGENTS: **`A-CHRONICLER` first — build the witness before the judge** → `A-LEDGER` → `A-PARENT` → `A-GATE` → `A-SCORER` → `A-DEVIL` cross-provider (the council's own ρ→1 disease, cured cheapest early) → analysts → `A-STRATEGY` last.
TASKS: `T-KEYS` — **rotate to read-only now; you don't need an inventory to revoke, discovery was never a prerequisite** → `T-COMP` → `T-LEVER` → `T-LEDGER` → `T-VERIFY` → `T-AMEND` → `T-THETA` → `T-SCORING` → `T-ENGINE` → `T-GATE` → `T-INDEP` → `T-AGENTS` → `T-REVIEW`.
*Comp:* position 2 in both queues — cheapest and fastest item on either list, and it shrinks everything downstream. **The Principal built this incentive himself; it is dissolvable by contract rather than governed by machinery.**
*Weakness:* consent-first can become consent-*forever* — a Principal who reads the giving-up list may decline the whole system, and the council would have talked him out of protection he needed. Also `T-KEYS`-before-`T-LEDGER` assumes rotation is operationally trivial; if Freedom Armenia cannot issue read-only keys, that ordering inverts.

**Member R** — *Principle:* descending artifact half-life, ascending reversibility. **What a stronger model makes *worse* comes first; what a stronger model makes *obsolete* comes last.** Facts about counterparties and human incentives are capability-invariant; agents are the shortest-lived object in the system.
RULES: 1 `R-CRED` (the only failure whose blast radius grows monotonically with capability) · 2 `R-LEVER` · 3 `R-COMP` (**capability-invariant defect that scaling amplifies: better agents give an option-holder more fluent justification for each override**) · 4 `R-OVERRIDE` · 5 `R-AMEND` · 6 `R-SOURCE` (its value rises with model fluency) · 7 `R-PARENT` · 8–12 rest. **`R-SILENCE`: demote hard — as frontier models converge, ρ→1 and silence becomes the base rate, not a signal; it fires false-negative by construction until cross-provider diversity is measured.**
AGENTS: `A-LEDGER` → `A-PARENT` → `A-GATE` → `A-CHRONICLER` → **`A-SCORER` — highest half-life of any component: the one artifact surviving every model upgrade, letting each new generation be re-run against a fixed registry** → `A-OVERLAP` → `A-DURATION` → `A-DEVIL` (only if genuinely cross-provider; provider diversity is a depreciating asset) → analysts last, cheapest to rebuild.
TASKS: `T-KEYS` → `T-LEDGER` → `T-LEVER` → `T-COMP` → `T-VERIFY` → `T-ENGINE` → `T-GATE` → `T-AMEND` → `T-THETA` → `T-SCORING` → `T-INDEP` (pull forward if a non-Anthropic reviewer is available now) → `T-AGENTS` → `T-REVIEW`.
*Comp:* wave one. **An option-like payoff is the one defect capability scaling strictly worsens — every improvement in the analysis layer hands the variance-seeking party a better argument. Fix the payoff before you build the persuasion engine.**
*Weakness:* may be overweighting capability trend; this is retrieval-plus-arithmetic, not a frontier system. If NAV is small relative to the €20k/€22k ceilings, the whole custody block is over-sequenced and `T-COMP` should be item 1.

---

# LIVE ORDERING DISPUTES (coordinator's scan of Round 1 — engage at least one)

1. **What occupies position 1 in RULES.** Most say `R-CRED` (code, zero dependency, closes the
   irreversible machine channel). Member F says `R-OVERRIDE` — the technical channel needs no
   override; what gets overridden is *rules*, and the man paid on quarterly variance cannot be the
   sole author of the exception. Member Q says `A-CHRONICLER` precedes everything: build the witness
   before the judge.

2. **Where `R-COMP` / `T-COMP` sits.** Wave one, positions 2–4 (A, B, J, P, Q, R — "delete the
   distortion instead of building governance against it"). Versus parallel and explicitly
   non-blocking (D, F, I, L — D calls gating on it a *shifting-the-burden trap*; F says Dmytro can
   stall it indefinitely because his option value is worth more unfixed). Versus Member C, who warns
   the council will rank it first purely from **availability bias** — it is the newest, most vivid
   fact, and its magnitude is unknown until high-water mark, clawback and realized-vs-mark are
   answered.

3. **Who owns `T-LEDGER`.** Session 1 assigned it to Dmytro. Members B, K and O independently say
   this is now a defect: concentration = variance = his upside, so he is the wrong attestor of the
   measurement that governs him. K wants it broker-attested.

4. **When `T-KEYS` happens relative to disclosure.** Member M argues rotation must land *silently,
   before* the compensation conversation, or Dmytro gets one quarter's warning to maximize variance
   — and prices the trust cost of that as unpaid. Member Q argues you never needed the inventory to
   revoke at all: rotate today, discovery was never a prerequisite.

5. **How many objects should exist.** Members O, P, K, E and Q each move to delete or reclassify
   items: `R-SILENCE` (monitoring signal, not a gate), `R-EXIT` and `R-COMP` (Principal decisions,
   not system rules), `R-SIZE` (½-Kelly on an unestimable edge is fake precision), `R-CASH`
   (a position with guaranteed real drag), `A-STRATEGY` (the four humans are the synthesis layer).
   Member P: "thirty-nine new objects for a system diagnosed as over-structured is the previous fix
   generating the next problem."

6. **`R-NOSTOP` is a conclusion, not a rule** (Member K). It holds only if leverage is zero and no
   forced-sale obligation exists — never established. Ranking it early removes a protection before
   its premise is verified. Member H ranks it *deliberately* early anyway, because the panic sale
   happens before the sophisticated rules ship.

7. **A newly discovered interaction** (Member K): if quarterly growth is measured on *realized*
   trades, the payoff rewards never selling losers — which is exactly what `R-NOSTOP` permits.
   Two individually sound decisions may combine into a mechanism for accumulating unrealized losses.

---

# ROUND 2 — key movements (de-anonymized for synthesis)
Mapping: A=Taleb B=Munger C=Kahneman D=Meadows E=Ada F=Machiavelli G=Karpathy H=Aurelius I=Torvalds
J=Aristotle K=Socrates L=Feynman M=Sun Tzu N=Musashi O=Rams P=Lao Tzu Q=Watts R=Sutskever

## Position changes with a NAMED flaw (genuine belief revision)
- **Kahneman** moved `T-KEYS` to 1. Named flaw: *attribute substitution* — "I answered 'what must we know first?' because it is easier than 'what can we close first?'" Credited Watts.
- **Taleb** dropped `R-NOSTOP` out of the early queue. Named flaw: "placing a rule above the verification it depends on, which my own stated principle forbids." Also raised `A-CHRONICLER`: "I gated the log on 'first LLM token', but overrides occur at the gate, which is not an LLM — my criterion under-fired."
- **Aristotle** moved `R-LEVER` 5→2, `R-COMP` 2→3, dropped `R-NOSTOP`. Named two flaws: `R-NOSTOP` mis-genused as a definition when it is a conditional; and `T-LEDGER` "attested by the party it governs is testimony, not material."
- **Sun Tzu** kept positions, changed the ledger's source. Named flaw: "I mapped the terrain but trusted the enemy's cartography."
- **Ada** de-serialized `A-CHRONICLER` to run parallel with `A-LEDGER`. Named flaw: "I over-serialized two independent modules" — they share no input symbols.
- **Watts** dropped `R-NOSTOP`. Named flaw: "I ranked it as a free deletion, importing a Session-1 *conclusion* as a premise."
- **Lao Tzu** moved `R-NOSTOP` 3→4. Named flaw: "I priced the subtraction in isolation… subtraction is not automatically safe."
- **Aurelius** moved `R-COMP` 10→3. Named flaw: "I called this an authorship problem, then ranked the authorship fix tenth." Also moved `T-KEYS` 2→1: "rotation binds all four equally; it is hygiene, not ambush."
- **Machiavelli** conceded `R-CRED` to position 1 (code needs no one's consent, his `R-OVERRIDE` does) but held `R-COMP` outside the top 5, endorsing Kahneman's availability-bias objection against his own side.
- **Meadows** moved `R-AMEND` above `R-OVERRIDE`. Named flaw: "I'd ranked the gameable version above the load-bearing one."
- **Rams** moved `A-CHRONICLER` above `A-GATE`. Named flaw: a gate deciding before logging exists produces its first decisions with no audit trail.
- **Sutskever** moved `A-CHRONICLER` 4→3. Named flaw: "I ordered it by artifact half-life and treated it as infrastructure rather than as the gate's own evidence."
- **Feynman** promoted `R-LEVER` to 2. Named flaw: "I let it hide inside a bucket instead of testing it directly."
- **Socrates** accepted the availability-bias objection against his own `T-COMP` placement, and added a new task: **ask the three compensation sub-questions (HWM, clawback, realized-vs-mark) — one email, no build, no negotiation** — separating the *question* from the *restructuring*.
- **Karpathy** accepted broker-attestation. Named flaw in his own domain language: letting Dmytro author the ledger is *train/test contamination*.
- **Munger, Torvalds** held positions; refined wording only (attestor, silence constraint, acceptance criteria).

## Substantive discoveries in Round 2
- **The composition bug (Socrates, adopted by Torvalds, Taleb, Lao Tzu, Meadows, Aurelius):** if quarterly growth is measured on *realized* trades, the payoff rewards never closing losers — exactly what `R-NOSTOP` permits. Two individually defensible rules compose into a mechanism for warehousing unrealized losses.
- **`R-COMP` is a category error in the rule pool (Aristotle, Ada, Socrates, Rams, Torvalds).** It has no runtime predicate `G` can evaluate; it is a contract term, not an invariant. It belongs in TASKS.
- **Negotiation ≠ consent (Aristotle, Lao Tzu, against Machiavelli).** Compensation is the Principal's pen; it requires notice, not Dmytro's agreement. Misclassifying it as bilateral manufactured the stall used to justify demoting it.
- **Circularity (Watts, against Kahneman).** The three missing sub-facts are the *output* of `T-COMP`, not its precondition; waiting for them before running it is circular. Magnitude governs harm, not cost-of-removal.
- **Disclosure sequencing (Sun Tzu, Musashi, Munger, Machiavelli):** rotate credentials before the compensation conversation, or the option-holder gets a quarter's warning. **Countered by Rams on ethics** ("Dmytro is not the adversary — he is one of four users; a design that deceives its own user is dishonest") and **by Aurelius** ("rotation binds all four equally; it is hygiene, not ambush").
- **The one dissent on `T-KEYS`-first (Karpathy):** rotating before characterizing the system means no baseline — you cannot distinguish a legitimate integration you just broke from noise. Speed vs. baseline.
- **`R-SILENCE` is conditional, not dead (Sutskever, against his own R1 demotion):** it fires false-negative by construction while the devil's advocate shares a provider; it belongs immediately after a genuinely cross-provider adversary ships. **Meadows defends it as a rule**, not reporting: it measures whether the analyst pack's own loop has taken over.

---

# BORDA TALLY (18 ballots, equal weights)
```

=== RULES (max possible 144) ===
 1. R-CRED              144 pts  | on 18/18 ballots | 1st place x18
 2. R-LEVER              96 pts  | on 18/18 ballots | 1st place x0
 3. R-AMEND              93 pts  | on 18/18 ballots | 1st place x0
 4. R-OVERRIDE           87 pts  | on 18/18 ballots | 1st place x0
 5. R-COMP               81 pts  | on 16/18 ballots | 1st place x0
 6. R-PARENT             61 pts  | on 18/18 ballots | 1st place x0
 7. R-SOURCE             51 pts  | on 16/18 ballots | 1st place x0
 8. R-NOSTOP             14 pts  | on 10/18 ballots | 1st place x0
 9. R-SIZE                7 pts  | on  5/18 ballots | 1st place x0
10. R-NEW-W-CONSENT       6 pts  | on  1/18 ballots | 1st place x0
11. R-EXIT                3 pts  | on  2/18 ballots | 1st place x0
12. R-SILENCE             3 pts  | on  2/18 ballots | 1st place x0
13. R-PHASE               1 pts  | on  1/18 ballots | 1st place x0
14. R-NEW-L1              1 pts  | on  1/18 ballots | 1st place x0

=== AGENTS (max possible 144) ===
 1. A-LEDGER            142 pts  | on 18/18 ballots | 1st place x16
 2. A-CHRONICLER        117 pts  | on 18/18 ballots | 1st place x2
 3. A-PARENT            114 pts  | on 18/18 ballots | 1st place x0
 4. A-GATE               93 pts  | on 18/18 ballots | 1st place x0
 5. A-SCORER             72 pts  | on 18/18 ballots | 1st place x0
 6. A-DEVIL              56 pts  | on 18/18 ballots | 1st place x0
 7. A-RISK               32 pts  | on 17/18 ballots | 1st place x0
 8. A-OVERLAP            11 pts  | on  8/18 ballots | 1st place x0
 9. A-STRATEGY           10 pts  | on 10/18 ballots | 1st place x0
10. A-DURATION            1 pts  | on  1/18 ballots | 1st place x0

=== TASKS (max possible 144) ===
 1. T-KEYS              143 pts  | on 18/18 ballots | 1st place x17
 2. T-LEVER             120 pts  | on 18/18 ballots | 1st place x0
 3. T-LEDGER            110 pts  | on 18/18 ballots | 1st place x1
 4. T-COMP               85 pts  | on 17/18 ballots | 1st place x0
 5. T-VERIFY             77 pts  | on 18/18 ballots | 1st place x0
 6. T-THETA              36 pts  | on 16/18 ballots | 1st place x0
 7. T-INDEP              23 pts  | on  9/18 ballots | 1st place x0
 8. T-AMEND              20 pts  | on 10/18 ballots | 1st place x0
 9. T-ENGINE             19 pts  | on 10/18 ballots | 1st place x0
10. T-GATE                8 pts  | on  7/18 ballots | 1st place x0
11. T-SCORING             4 pts  | on  1/18 ballots | 1st place x0
12. T-AGENTS              2 pts  | on  1/18 ballots | 1st place x0
13. T-REVIEW              1 pts  | on  1/18 ballots | 1st place x0

=== DEALBREAKERS ===
R-NOSTOP           8
A-STRATEGY         4
T-LEDGER           2
T-THETA            1
T-COMP*            1
R-EXIT             1
R-SILENCE          1
```
