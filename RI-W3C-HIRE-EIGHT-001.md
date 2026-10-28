# Hiring-Agent Authority and Human Escalation: Independent Receiver Research

**Research type:** Bounded synthetic independent-receiver reproducibility exercise  
**Original record identifier and protocol examined:** RI-W3C-HIRE-EIGHT-001 v0.1 (frozen; filename and original evidence references preserved)  
**Proposed future identifier:** RI-INTEROP-HIRE-001 v0.2 (not issued, tested or published)  
**Run and technical review:** 27 October 2026  
**Publication status:** Authorised for publication: two verbatim reviewer documents and this scope/attribution index  
**Canonical research programme:** https://responsibilityinfrastructure.com/research

## Recorded result

| Dimension | Recorded result |
| --- | --- |
| Frozen synthetic case outcomes | 8/8 reproduced in Prasanna's reported non-blind run |
| Evidence-slot counts | 8/8 matched the frozen expected counts |
| Separate receiver built from protocol text | Reported completed |
| Re-run after removing issuer | Reported identical |
| Clean-directory re-run | Reported byte-identical |
| Specification gaps | Ten findings recorded |
| Blind validation of expectations | NOT PERFORMED |
| Full RI conformance or live operational validity | NOT ESTABLISHED |

These are claims of the **authored findings and run report**, not a separate La Touche re-execution or certification of the receiver implementation. The reviewer saw the expected results in the protocol before implementing the receiver. Matching those expected results demonstrates bounded independent reproducibility under the stated assumptions, not correctness of the expectations. No external-system production integration is established.

## Research question and finding

Can a separately implemented receiver reconstruct the available evidence about historical hiring-agent authority and a human escalation, without turning missing, conflicting, wrong-role or time-inapplicable records into established authority, receipt, acknowledgement or acceptance?

The reviewer identified ten specification gaps relevant to v0.2, including reference format and resolution, outcome priority, evidence-slot counting, temporal evaluation and the distinct escalation-time narrowing case. In particular, the implemented H06 action-time narrowing case must not be treated as equivalent to Prasanna's proposed narrowing-between-escalation-and-acknowledgement case.

## Attribution and independence

- **Prasanna Bableshwar** introduced the production-informed hiring use case, contributed three of the eight synthetic scenarios and testing-method requirements, and wrote the separate receiver's findings and run report. His contribution was in his **personal capacity only**.
- **Raphael A. La Touche** proposed five initial synthetic scenarios on 23 October 2026; **La Touche** prepared the v0.1 protocol and the initial internal experiment.
- The reviewed synthetic case set and technical requirements reflect distinct contributions. A shared research question does not make the reviewer a joint author of the v0.1 document.

No actual candidate data or proprietary Atlassian material was included in this published record. This is **not** an Atlassian position or endorsement, a W3C publication or endorsement, a conformance assessment of RI-STD-01, a blind interoperability result, or a validation of the La Touche commercial product.

## Author-approved reviewer publications

The following two files are published **verbatim, as authored**, with the stated scope and limitations. Read the complete report rather than extracting results without context.

- [Prasanna's findings — verbatim](./RI-W3C-HIRE-EIGHT-001-findings.md)
- [Prasanna's run report — verbatim](./RI-W3C-HIRE-EIGHT-001-run-report.md)

Prasanna explicitly approved publication of his findings and run report on 27 October 2026, in personal capacity, with non-endorsement boundaries. He subsequently required verbatim publication and approved the attribution/evidence statement.

**Excluded from this permission:** receiver source code, executable artifacts, fixtures, native records, results files and their licence. Publication of those requires a separate agreed file-by-file inventory, privacy decision and licence. A referenced path inside an authored report does **not** make that underlying file public or authorised for release.

**Licence statement:** Specific rights or an open-source licence for the independently authored files have not been granted by this publication approval. Attribution and permission to publish these exact works should not be read as permission to modify or redistribute them under an unspecified licence.

**Publication boundary:** This is a separate bounded synthetic receiver-reproduction study, **not** a sixth published external-system interoperability test. It is not counted in the five external-system tests reported on the RI site.

© 2026 La Touche Holdings Ltd for this editorial record. Author ownership and rights in the verbatim reviewer reports remain with their respective author.
