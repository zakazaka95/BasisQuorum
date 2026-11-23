# BasisQuorum reproducible Studio walkthrough

This is the reproducible procedure. Actual execution results are recorded separately in [DEPLOYMENT.md](DEPLOYMENT.md); an expected branch below is not evidence that it occurred. Use only synthetic technical reports and zero transaction value. Network fees may still apply. Never substitute a prior contract address for this source.

## Before deployment

1. Check the current official Studio network, compiler and dependency compatibility. The release pins `# v0.4.0` and `py-genlayer:kzybg95x1gn21dw72m7hyg0maaap04n4nx55j9yt6fkdqxtz6bz0`; do not silently deploy a different version.
2. Run the 41 local tests. Verify `BasisQuorum.py` SHA-256 against `DEPLOYMENT.md`. If any source byte changes, rerun the relevant checks, update the fingerprint and repeat the matching-source review.
3. Use the complete reviewed code, tests and documentation. Record an immutable commit link to the exact source and its fingerprint.
4. Deploy the whole standalone `BasisQuorum.py` with no constructor arguments and no attached value. Wait for the actual accepted/final state required by that network. Record deployment transaction and contract address. A submitted transaction alone is not a successful deployment.
5. Call `get_stats`. Check `contract_version=1.0.0`, `receipt_schema=basisquorum-v1`, `max_reports=6`, `max_reporters=8` and `max_attempts=3`. Confirm initial collection/report/assessment counters are zero.

## Synthetic bridge demonstration

All following descriptions are deliberately synthetic. They assert no actual CI job was performed. Let the connected wallet be the owner and sole reporter.

Call `open_collection` with these arguments:

| Argument | Value |
| --- | --- |
| `title` | `Synthetic parser evidence quorum` |
| `claim` | `In this synthetic fixture, parser P rejects malformed token X.` |
| `independence_standard` | `Count separately executed test runs with separate produced outputs as distinct. The same claim, code or test specification does not alone mean a shared run. A report reusing a run's produced output shares its basis with that run. A combined analysis reusing two runs' outputs overlaps both. Unknown separation is uncertain. This is declared lineage accounting only.` |
| `reporters_json` | `[]` (JSON text string, not an omitted argument) |
| `quorum` | `2` |

Save the actual returned collection ID as `C`; do not assume zero on a previously used deployment.

Call `append_report(C, report_text, basis_text)` twice:

| Field | First report | Second report |
| --- | --- | --- |
| `report_text` | `Synthetic fixture report A: execution A records parser P rejecting malformed token X.` | `Synthetic fixture report B: execution B records parser P rejecting malformed token X.` |
| `basis_text` | `Synthetic execution A produced output A in its own fresh run. Output A is not copied from another report or execution. No other output is used.` | `Synthetic execution B produced output B in its own fresh run. Output B is not copied from another report or execution. No other output is used.` |

Call `get_collection(C)` and copy the exact `revision` and `snapshot_hash`. Call `assess_revision(C, revision, snapshot_hash)` as owner. If consensus agrees on two distinct support components and complete coverage, the deterministic expected decision is `SUPPORTED`, with two support units. Inspect the full stored receipt and both reports, and verify `get_current_certificate(C)` matches its revision/hash and receipt hash. Record the actual accepted result and transaction. If independent assessments disagree or return uncertainty, record that honestly; do not present the expected branch as observed.

Now append a bridge:

| Field | Value |
| --- | --- |
| `report_text` | `Synthetic fixture report C: a combined analysis of outputs A and B also supports parser P rejecting malformed token X. It is not a third test execution.` |
| `basis_text` | `This combined report directly reuses exact produced outputs A and B from the two earlier declared runs. It adds no independent run or produced output. Its declared basis overlaps both report A and report B.` |

Immediately, **before assessing the new revision**, `get_current_certificate(C)` must error. `get_revision(C, old_revision)` must still return the previous historical certificate. Read the new exact revision/hash and assess again. If semantic consensus returns support for all reports, `SHARED_BASIS` links from C to both A and B, and `whole_set=COMPLETE`, the deterministic result is one connected component, one support unit and `NO_QUORUM`. The A/B `DISTINCT_BASIS` label cannot split that transitive component. This is a conservative representation, not a claim that appending text changes external reality.

## Additional branches on fresh collections

The release demonstrated the primary bridge flow and the retirement/history
branch below. Other bullets remain optional procedures; the local suite covers
them, but they are not represented as executed network negatives unless an
actual transaction is recorded in DEPLOYMENT.md. Current-certificate native
views expose generic `execution failed` on this host; the public proof combines
that observed rejection with successful adjacent state/history reads rather than
claiming the provider exposed a specific contract error reason.

- Duplicate the exact basis string through two authorized wallets. Even with semantic `DISTINCT_BASIS`, the receipt's effective link must be `SHARED_BASIS` with reason `IDENTICAL_BASIS_TEXT`; different wallets do not prove independent origin.
- Use explicitly overlapping declared basis descriptions with different wording and verify shared links when consensus recognizes them. Inspect both the semantic and effective pair lists.
- Use a clearly conflicting support/refute collection. The expected deterministic outcome, when those stances are agreed, is `CONTESTED` and no certificate.
- Use insufficient, ambiguous or missing declared basis context. `UNDETERMINED` stances or `whole_set=UNCERTAIN` must never produce a certificate. Pair-level `UNCERTAIN` merges components; it does not unconditionally veto an otherwise sufficient merged quorum.
- After any readable decision, attempt the same revision again. It must reject before another semantic assessment. Do not spend repeated network fees trying to force a different verdict.
- Try an unauthorized writer, nonowner assessment, stale revision/hash and seventh report. Each must reject and leave state unchanged. Record only genuine observed errors.
- Retire an assessed collection as owner. The current certificate must become unavailable immediately, further appends/assessment must reject, and historical receipts must remain readable.

Local tests cover forced malformed output, independent disagreement, all receipt-leaf tampering, reverse clock and full maximum-source prompt budgets. These controlled cases are not equivalent to inducing all those branches in Studio; do not label them live tests or model benchmarks.

## Evidence to preserve

Record the exact source commit + SHA-256, Studio network/chain identifier, matching Explorer contract URL, deployment transaction, accepted assessment transaction(s), actual full receipt(s), current revision/hash before and after the bridge and retirement result. Confirm the Explorer source bytes match the submitted source. Add real links to `DEPLOYMENT.md` and the Portal evidence only after they exist. Portal copy must describe the actual demonstrated outcome.
