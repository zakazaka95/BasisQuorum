# BasisQuorum — November 23 release record

Published **November 23, 2026**. Current native source-schema validation, the
complete controlled-output local suite and matching deployment succeeded. The
complete deployed source and initial stats were verified. The two-report revision
was `SUPPORTED`; the appended bridge immediately revoked its current use, and
reassessment produced the expected deterministic `NO_QUORUM`. Retirement also
succeeded while preserving both historical receipts and the original certificate.
All eight transactions were successful and `FINALIZED`. Portal status remains
separate evidence and no award is claimed.

| Item | Current evidence |
| --- | --- |
| Contract version / receipt schema | `1.0.0` / `basisquorum-v1` |
| Exact released source SHA-256 | `0983bf98113420a1d0803d1beee09bde48298a655477237ed933f9525a7c60db` |
| Public repository | https://github.com/zakazaka95/BasisQuorum |
| Immutable source | https://github.com/zakazaka95/BasisQuorum/blob/088255dd60eef3bbb68a18c46eea14944dcfaf00/BasisQuorum.py — independently retrieved exact raw bytes match |
| Local suite on released source | 41 passing controlled-output tests |
| Native source-schema validation | Passed with the pinned v0.4.0 runner during this release |
| Constructor / transaction value | No constructor parameters; synthetic writes use 0 GEN value; network fees are separate |
| Network / chain ID / RPC | Studio Devnet / `61997` / `https://studio-dev.genlayer.com/api` |
| Contract | [0xdedd9cfd730fa93b7c1Bd7F8D5d0cFC60F505fc3](https://explorer-studio-dev.genlayer.com/address/0xdedd9cfd730fa93b7c1Bd7F8D5d0cFC60F505fc3) |
| Deployment transaction | [0xdcfe2fd55f85e76ea19639e8a660a93a62a0fc8a07e57a6dd6e9bd6e0e46c0f8](https://explorer-studio-dev.genlayer.com/tx/0xdcfe2fd55f85e76ea19639e8a660a93a62a0fc8a07e57a6dd6e9bd6e0e46c0f8) — successful execution |
| Complete tracked/deployed source comparison | Full source matches after CRLF-to-LF conversion and outer-whitespace trim; normalized SHA-256 `49d9d773a5f1b81479ea92949ae0dfb24e1ea925f72f7362097b3c3af845bb49` |
| Initial persisted readback | `get_stats` retrieved successfully after deployment |
| Initial application state | Collection and two synthetic reports persisted; revision `2` was read before semantic assessment with `UNASSESSED` and zero attempts |
| Demonstrated collection | Collection ID `0`; reports `[0, 1, 2]`; quorum `2` |
| Initial semantic assessment | [Revision 2 assessment succeeded](https://explorer-studio-dev.genlayer.com/tx/0x150d756a90fc03f9f31cfe3a99b75f9b2922fa60320c69b73f5ea199c25bb822), storing `SUPPORTED` with two separate complete support units |
| Initial scoped certificate | Retrieved successfully for revision `2` before the bridge append |
| Revision 2 receipt SHA-256 | `56d961f8261e3aedbe8ddcd45baa2bb70febad29b60a9710f17928721876f7cc` |
| Immediate bridge invalidation | [Bridge append succeeded](https://explorer-studio-dev.genlayer.com/tx/0xd75cf1a834cf28ec1fed52d60fff33c5e2fa9a62517693abf79ef11f331a375c), creating revision `3` with `UNASSESSED` state and `certificate: null`, before any assessment of that revision |
| Historical certificate after append | Revision `2` remains `SUPPORTED` with its original historical certificate |
| Native current-certificate view | Rejected with generic `execution failed`; no specific guard reason was exposed by the provider. Adjacent stored-state readbacks verify revision 3 and the absent current certificate |
| Bridge semantic reassessment | [Revision 3 assessment succeeded](https://explorer-studio-dev.genlayer.com/tx/0x7a96250484140977bd745cf2140bd439e0503589e042d93a1f1412f096790a29), storing `NO_QUORUM` with complete coverage |
| Revision 3 receipt SHA-256 | `8e28dd9e2aaa9044eaed91ffcc5257b5c24cf41ac477f615adf762f80e593852` |
| Transitive component readback | One support component `[0, 1, 2]`, one support unit against quorum `2`; the bridge shares basis with both earlier reports |
| Current versus historical result | Revision 3 has no current certificate; revision 2 remains historical `SUPPORTED` with its exact original certificate |
| Retirement and history | [Owner retired the collection](https://explorer-studio-dev.genlayer.com/tx/0x35fbec6e32b48027bc4cd86cdb50b7b497e044c3dee4bcf309df9d58f89bb53e); both historical receipts and the original revision 2 certificate remained unchanged |
| Transaction finality | All eight tracked synthetic transactions successful and `FINALIZED`; complete proof collected November 23 at 16:29:52 UTC |
| Portal contribution ID / status | Not submitted yet; no award claimed |

## Minimal runner migration

The archived prepared source pinned v0.3.0. The current release changes only the
first two runner-header lines to the native-verified pin:

```text
# v0.4.0
# { "Depends": "py-genlayer:kzybg95x1gn21dw72m7hyg0maaap04n4nx55j9yt6fkdqxtz6bz0" }
```

The contract body, API and consensus/state logic are unchanged. All 41 local
tests passed on this released source, separately from native source-schema
validation. The archived prepared raw source SHA-256 was `506f29bb29730ee575fbbc782cf4614e3ad161abbc0918c9c2ecd952ce13371f`; it is historical,
not the released source identified by the current hash above.

Raw file-byte hashes are distinct from any separately normalized complete
Explorer-source comparison. The complete comparison and normalization rule are
recorded above. Schema validation and initial stats alone do not establish a
successful application write, transaction-clock behavior or semantic correctness.

## Reproduce and interpret the evidence

The public [complete demonstration](evidence/demo-result.json),
[transaction list](evidence/transactions.json), [native schema result](evidence/native-schema.json)
and [complete source comparison](evidence/source-verification.json) preserve both
full semantic receipts, immediate invalidation, historical-certificate retention,
retirement and the verified transaction finality.

The [RPC recovery record](evidence/rpc-recovery.json) separates provider rate-limit
declines before a hash from tracked onchain transactions. Nonces and persisted
state were reconciled before resuming; no hidden assessment or repeated verdict
was inferred from those offchain declines.

Use [STUDIO-TEST.md](STUDIO-TEST.md) with synthetic technical declarations,
normal consensus and zero transaction value. Require successful execution and
persisted application state, not acceptance alone. Preserve readable adverse
outcomes and distinguish local controlled-output tests, actual semantic results
and transaction finality. Neither a unit suite nor a small synthetic walkthrough
is a model-reliability benchmark or a production-readiness guarantee.

The complete walkthrough identifies collection revisions and snapshot hashes,
full assessment receipts, the initial current certificate, immediate invalidation
on append before reassessment, immutable history and the transitive bridge result.
Certificates concern declared bases under the chosen
standard, not verified origins, unique humans or statistical independence.
