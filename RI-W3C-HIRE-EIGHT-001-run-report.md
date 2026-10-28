# Run report: eight-case independent receiver test

Protocol under test: RI-W3C-HIRE-EIGHT-001 v0.1, as reproduced in the task file. The frozen expected observations and slot counts in the case definitions are the oracle. Nothing in the oracle was changed during the run.

## Implementation and versions

- Implementation: latouche-eight-case-run 1.0, in this directory.
- Runtime: Python 3.12.3.
- Dependencies: Python standard library only. No vendor products. No network access used or needed.
- Parts: an issuer (issuer/build_records.py), an independent resolver (resolver/resolver.py) and a scoring harness (run.py). The harness runs the issuer and the resolver as separate processes.

## Inputs

- Eight case definitions in cases/, one per case H01 to H08. Each carries the setup events with instants, the synthetic reference and record inputs, the frozen expected observation and the expected slot count.
- All data is synthetic. The designated role is designated-reviewer. The wrong role in H08 is team-member. The single action is screen-candidate.

## Reference and record shape chosen

The protocol carries no reference format, so this run chose a minimal one and records the choice here. A reference is a record identifier plus the designated role. A record is a JSON object holding the record identifier, the designated role, the authority versions with scope and validity interval, the fetch behaviour for the case and the event list in instant order. Authority versions carry a change_type field with values issuance, narrowing and revocation, because the protocol has no field that distinguishes revocation from narrowing. The resolver receives the reference and the record. It receives nothing else.

## Results

| Case | Resolver outcome | Expected outcome | Authority | Slots evidenced | Expected slots | Record SHA-256 |
| --- | --- | --- | --- | --- | --- | --- |
| H01 | POSITIVE_CHAIN_COMPLETE | POSITIVE_CHAIN_COMPLETE | ESTABLISHED | 6/6 | 6/6 | 10a14455568ced088b998296bd91d37b5f1dcf7d9fa8af74ba68c8c8a034dd20 |
| H02 | ISSUED_NO_RECEIPT_EVIDENCE | ISSUED_NO_RECEIPT_EVIDENCE | ESTABLISHED | 3/6 | 3/6 | d01961a56747e3accddb8ae0da58fd78edcc9633b04e409e3fcbb108b35a7620 |
| H03 | ACKNOWLEDGED_NO_ACCEPTANCE_EVIDENCE | ACKNOWLEDGED_NO_ACCEPTANCE_EVIDENCE | ESTABLISHED | 5/6 | 5/6 | 7cef35bf3b48a65d34ce0f36c6198e6d4df9c4c4a1dd83c7c31e08c461096dde |
| H04 | RECEIVED_NO_DESIGNATED_ACK | RECEIVED_NO_DESIGNATED_ACK | ESTABLISHED | 4/6 | 4/6 | 5feb38062d26f0299622d6d37d9fb0aa4cd46bf12676a9d668ef9a3aa447dcd7 |
| H05 | NOT_ESTABLISHED | NOT_ESTABLISHED | NOT_ESTABLISHED | 5/6 | 5/6 | ef37f431a757ca346ae75fa4346d2a84addcd66aabe6ccfc3dcb255257126a51 |
| H06 | SOURCE_SCOPE_DENIES | SOURCE_SCOPE_DENIES | ESTABLISHED | 5/6 | 5/6 | 448b283b744cac49dd7adf35eb9b0d9553f9eadad656eb62b2a27a6f7d663d5d |
| H07 | FAIL_CURRENT_FOR_HISTORICAL | FAIL_CURRENT_FOR_HISTORICAL | NOT_ESTABLISHED | 5/6 | 5/6 | 481961fc7aeae9d03bec0d83450f1b96f681690351b50ed845cd957757d387a8 |
| H08 | WRONG_ROLE_ONLY | WRONG_ROLE_ONLY | ESTABLISHED | 4/6 | 4/6 | 3e8142537a5179450bbc74772431b036acc1b8a631d3496f2d5a2255c8131819 |

All eight cases matched the frozen oracle on outcome, on authority status and on evidenced slot count. Full per-case detail is in results.json. The resolver output is in audit.json. The records are in records/.

One honesty note. This run was not blind. The person directing it had read the expected outcomes before the run, because the protocol text is the task. The run therefore validates that an independent implementation can reproduce the expected results from the record alone. It does not validate the expectations themselves. That question is handled in findings.md.

## Acceptance criteria, checked one by one

1. All eight case definitions exist and carry the frozen expected observation and slot count exactly as in the protocol text. Pass. Where the protocol states an observation in prose (H01 and H05), the case file records that fact and the tokenization used, fixed before the run.
2. The resolver reconstructs from the record alone. Pass, tested two ways. The resolver source contains no import of the issuer and no shared code path with it. In the reproduction directory the issuer directory was deleted after the records were written and the resolver was run again on the records alone. Its output was identical.
3. H05 and H07 return NOT_ESTABLISHED for source action authority. Pass. Neither returns a silent empty result and neither substitutes the current version. H07 returns the distinct outcome FAIL_CURRENT_FOR_HISTORICAL with authority NOT_ESTABLISHED.
4. H02, H04 and H08 record missing evidence as missing. Pass. H02 evidences no receipt, no acknowledgement and no acceptance. H04 evidences no acknowledgement and no acceptance. H08 evidences no designated acknowledgement and no acceptance, and the wrong-role acknowledgement is preserved as a wrong-role acknowledgement.
5. The run reproduces from a clean checkout in an empty working directory. Pass. The cases, issuer, resolver and harness were copied to a fresh empty directory with no prior outputs and run there. The resulting results.json was byte-identical to the main run. SHA-256 of results.json in both runs: 96d574ece09c9a4d024e02bc2a495195e946287f404248f99c3ff824f8480d20.
6. findings.md answers all three review questions and carries protocol-gap entries tied to cases. Pass. See findings.md.

## What was not run

No mutation controls were added. The author's internal run used four, but the protocol text does not specify them, and adding controls would extend the oracle surface beyond the frozen text. This is recorded in findings.md as a gap in the protocol, not filled silently here.
