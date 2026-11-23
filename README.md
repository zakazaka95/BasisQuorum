# BasisQuorum

A bounded quorum primitive for **complete declared evidence bases**, so six copied reports do not automatically become six units of support.

**Published November 23, 2026.** Current native source-schema validation, all 41 controlled-output tests and the source-matched deployment succeeded. Application results are recorded only as observed in [DEPLOYMENT.md](DEPLOYMENT.md). There is no frontend, asset transfer, reputation penalty, live evidence feed or paid action.

The release pins the native-verified v0.4.0 runner. Only the two runner-header lines changed from the archived preparation; the contract body is unchanged. The [immutable contract source](https://github.com/zakazaka95/BasisQuorum/blob/088255dd60eef3bbb68a18c46eea14944dcfaf00/BasisQuorum.py) was independently retrieved and matches the exact released file bytes.

The [live demonstration](evidence/demo-result.json) records a two-unit `SUPPORTED` certificate, its immediate invalidation on bridge append, the expected one-component `NO_QUORUM` result and retirement with historical receipts preserved. All eight transactions succeeded and reached `FINALIZED`.

## What it records

An owner freezes one exact technical claim, a complete declared independence standard, a quorum of 1–6 and a fixed list of authorized reporters including the owner. Each report records the authenticated sending wallet, its complete report text and its complete asserted basis text. Reports are append-only; exact copies are deliberately allowed.

GenLayer's semantic task assesses every report's stance, every unordered pair's declared basis relationship and whether the whole set can be conservatively represented. Deterministic code computes connected components and the final scoped decision. The meaningful state is the immutable collection specification, full revision snapshots, accepted attempt receipts, bounded failure lifecycle and a revocable current-revision certificate.

A useful integration is a technical review workflow that needs a declared-basis quorum before advancing. Three people quoting one CI job must not masquerade as three separate tests. Conversely, a bridge report can show that previously separate basis components overlap, reducing the quorum. This is deliberately conservative accounting, not a statistical estimate of evidence independence.

## Decision rules

Each report must receive `SUPPORT`, `REFUTE` or `UNDETERMINED`. Every unordered pair must receive `SHARED_BASIS`, `DISTINCT_BASIS` or `UNCERTAIN`, with exact real report IDs and complete coverage in the supplied order. `whole_set` is `COMPLETE` or `UNCERTAIN`; the latter is required if material joint/indirect dependencies or missing context cannot be safely represented by those links.

1. Identical exact basis strings are deterministically linked as `SHARED_BASIS`, even if the semantic output calls them distinct. The receipt retains both semantic and effective links, with the override reason.
2. `SHARED_BASIS` and `UNCERTAIN` links both merge components transitively. A `DISTINCT_BASIS` endpoint label never splits an existing chain. Pair-level uncertainty therefore reduces possible units; it is not by itself an unconditional veto.
3. Each uniform support or refute component contributes at most one unit. A component containing both support and refute is mixed. Any component containing an undetermined stance is unresolved unless it is already mixed.
4. Any mixed component, or both support and refute components, yields `CONTESTED`.
5. Otherwise, uncertain whole-set coverage or any unresolved component yields `INCONCLUSIVE`.
6. Otherwise, support units reaching the frozen quorum yield `SUPPORTED`; refute units reaching it yield `REFUTED`. Any smaller total yields `NO_QUORUM`.

Only `SUPPORTED` and `REFUTED` have a scoped certificate. `CONTESTED`, `INCONCLUSIVE` and `NO_QUORUM` are readable final semantic decisions for that exact revision, not technical retry opportunities.

## Complete consensus binding

The leader and independent validator each receive the complete same claim, standard, report metadata, report texts, basis texts and all pair identities. They independently execute the semantic task and rebuild the **entire canonical receipt**, including the source snapshot, author identities, timestamps, prompt character/byte counts and digest, coverage flags, every stance, every pair, effective overrides, components, counts, final decision and certificate payload. Validation requires exact canonical JSON equality. Matching only the verdict or source hash is insufficient.

Input strings remain untrusted data within the prompt; no report content authorizes tools, browsing or external actions. Exact equality demonstrates agreement for the complete result; it does not prove semantic accuracy or immunity to prompt injection. Different independent classifications are rejected rather than quietly stored. Such a rejected consensus does not consume a contract-level accepted attempt.

## Lifecycle and integration boundary

The first collection revision is empty and cannot be assessed. Every accepted append creates a new full snapshot and immediately removes availability of the old live certificate, even before another assessment. A new revision may legitimately receive a different decision. Prior snapshots and accepted receipts remain readable only as history.

Assessments are owner-only and require the exact current revision and snapshot hash. A malformed output or prompt failure produces a fail-closed `UNRESOLVED` receipt. At most three such accepted attempts are allowed per revision, ending in `UNRESOLVED_FINAL`; a readable semantic decision is final immediately. There is no same-revision verdict shopping. Retrying does not overwrite earlier attempt receipts. Consensus rejection and network failure are outside this accepted-attempt counter and may incur future network fees if a caller keeps retrying.

The owner may irreversibly retire the collection. Retirement blocks all further reports and assessments and revokes live certificate access. Historical receipts remain readable. There is no withdrawal, editing, reporter replacement or slot recovery; a correction is another full report within the six-report lifetime cap. An authorized reporter can exhaust those slots, so the list is a real trust boundary.

Consumers must pin the contract address and collection, read `get_collection` and `get_current_certificate`, and bind the current revision and snapshot hash. A stored historical certificate, an earlier response or a UI cache is not a current authorization. A separate read followed by a later external action has a race; an integration must enforce a current-version guard at its own point of use. The contract does not execute external releases itself.

## Scope limits

- Reports are synthetic or caller-supplied technical declarations, not web-fetched, authenticated test artifacts. Wallet authentication identifies the writer, not the true report origin, a unique human or a unique real incident.
- `SUPPORTED` means an agreed quorum under this exact declared-basis representation. It does not prove the outside claim true, the underlying evidence genuine or the sources statistically independent.
- Equal basis text is conservatively collapsed even when separate real tests happen to have identical descriptions. Semantically shared but differently worded bases still depend on the consensus task. A joint report may conservatively connect otherwise separate components.
- The owner chooses the claim, standard, quorum and allowed writers and controls when to assess or retire. This is a reusable coordination record, not permissionless discovery or a universal truth oracle. New collections do not silently replace an integration's pinned collection.
- Clock reads occur only in deterministic public methods. Every successful collection write advances a per-collection time floor; backward-time writes and live-state reads fail closed. Historical getters do not assert current validity.

## API

| Method | Authority and purpose |
| --- | --- |
| `open_collection(title, claim, independence_standard, reporters_json, quorum)` | Anyone creates a collection and becomes its owner. `reporters_json` is a JSON string containing 0–7 additional nonzero addresses; the owner is included automatically. Returns the collection ID. |
| `append_report(collection_id, report_text, basis_text)` | Frozen reporter only; returns a global report ID and creates a full new revision. |
| `assess_revision(collection_id, expected_revision, expected_snapshot_hash)` | Owner only; returns the independently agreed complete receipt. |
| `retire_collection(collection_id)` | Owner only, irreversible. |
| `get_collection(collection_id)` | Current specification, revision, snapshot hash, report IDs and retirement state. |
| `get_current_certificate(collection_id)` | Current live scoped certificate or an error. |
| `get_report(report_id)` | Immutable full report. IDs are global, so a collection can have noncontiguous IDs. |
| `get_revision(collection_id, revision)` | Historical snapshot, final/retry state, latest receipt and historical certificate. |
| `get_attempt(collection_id, revision, attempt)` | Immutable accepted receipt for that attempt, starting at 1. |
| `get_stats()` | Version, schema, counters and limits. |

Title is at most 100 characters; claim and standard 600 each; report and basis 500 each. There are at most six reports, 15 unordered pairs and eight authorized reporters including the owner. Inputs must be nonblank valid Unicode. Every append stages a full prompt budget check before any write. Prompts may not exceed 50,000 characters or 65,000 UTF-8 bytes; the contract refuses an over-budget source instead of slicing it. No callback reads the clock.

## Reproduce local checks

From this directory:

```text
python -B -m unittest discover -s . -p test_basisquorum.py -v
```

**41 controlled-output tests passed on November 8 and were rerun successfully on the released source November 23**, using `testsupport.py` as a storage/consensus double. The suite covers distinct/shared/transitive/uncertain components, bridge invalidation, contradictory components, symmetric refute quorum, whole-set uncertainty, global IDs, authority, limits, immutable history, retirement, reverse clock, bounded retries and independent disagreement. One test individually mutates **102 receipt leaves**, plus separate added/removed/reordered fields. Six maximum-sized report/basis pairs and maximum claim/standard lengths are parsed back from both independent prompts using astral Unicode and escaped controls, with no silent cutoff. These are local logic tests, not GenVM execution, a live deployment or AI reliability benchmarks.

The on-chain file imports no local helper. It pins the recorded `py-genlayer` dependency in its header. Native source-schema validation, real transaction execution and semantic behavior are separate checks. [STUDIO-TEST.md](STUDIO-TEST.md) provides the reproducible procedure; [DEPLOYMENT.md](DEPLOYMENT.md) records the exact released source fingerprint and observed network results. [SUBMISSION-PACK.md](SUBMISSION-PACK.md) contains the Portal description and matching evidence links.
