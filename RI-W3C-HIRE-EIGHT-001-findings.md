# Findings: eight-case independent receiver test

## Scope of this review

This is a bounded independent run of one synthetic protocol, RI-W3C-HIRE-EIGHT-001 v0.1. An independent resolver was built from the protocol text alone and run against the eight frozen cases. The run establishes what is stated in run-report.md and nothing more. It is not a conformance result for any standard. It is not an endorsement of RI-STD-01, of its author or of any product. The author's own status page records that full conformance of his framework is not established and that independent review is not yet complete. This run is one piece of that review, with the limits stated below.

One limit applies to everything here. The run was not blind. The expected outcomes are stated in the protocol text, so the implementer had read them before building. The run shows the expectations are implementable and reproducible by a second party. It cannot show the expectations are the right ones. The answers below separate those two claims.

## Question 1: Correctness

Are the eight expected observations and negative outcomes justified?

In substance, yes, with two qualifications. A resolver built independently from the text reproduced all eight expected observations and all eight slot counts without inferring any event the record did not evidence. The negative outcomes are the strong part of the protocol. H02 refuses to infer receipt from issue. H03 refuses to treat acknowledgement as acceptance. H04 keeps an unanswered referral unresolved instead of inventing approval or rejection. H08 refuses to count a wrong-role acknowledgement as a designated one. Each of those matches the underlying standard's own rules on acknowledgement and silence, and each was reached by the resolver from the record alone.

Qualification one, from H05 and H07. The protocol treats an unavailable historical reference and a substituted current version as different failures with different outcomes, NOT_ESTABLISHED and FAIL_CURRENT_FOR_HISTORICAL. That distinction is justified, because the remedy differs. But the protocol never states how a receiver tells the two situations apart. This run distinguished them by fetch behaviour in the record, a shape the protocol does not define. A second implementer could reasonably collapse the two cases into one outcome and still claim to follow the text.

Qualification two, from H01. The positive case is stated in prose and has no outcome token. Every negative case has a token. The protocol therefore specifies failure vocabulary more precisely than success vocabulary, and the one case that exercises the full chain is the one case whose expected output an independent implementer must tokenize for himself. This run used POSITIVE_CHAIN_COMPLETE and recorded the choice in the case file before running.

On over-inference: the cases are careful, and the run found no case that over-infers authority, receipt or acceptance from the evidence supplied. The residual risk is not inside a single case. It is between cases. The protocol gives no priority order for its outcome tokens, and real records can satisfy two at once. In H06 the record also satisfies the shape of H03 (designated acknowledgement with no acceptance) while the expected outcome is SOURCE_SCOPE_DENIES. This run applied authority and scope outcomes before referral chain outcomes. A different order gives a different headline outcome from the same record, with the same slot count. The protocol does not say which is right.

## Question 2: Measurability

Are the six slots, denominators and resolution criteria sufficiently precise for independent assessment?

Partly. The six slots are plain enough that a second party applied them and landed on the author's expected count in all eight cases, including the two partial reconstructions. The fixed denominator of six is a real strength: counts are comparable across cases in a way a per-case denominator would not allow.

Three precision gaps remain.

First, the six slots are defined by no artefact outside this protocol text. The W3C Agent Conformance Reporting Format v0.1 defines an evidence object with five slots, changed, fixed, compared, moved and delta. Those are different slots for a different purpose. The six-slot event reconstruction measure in this protocol is a separate construct, and nothing published defines it independently of these eight cases. Until it stands in a document of its own, every independent assessment is an assessment against a one-page protocol, not against a stable measure.

Second, the counting rule for slot 1 is unstated. In H06 the authority record covering the action time exists and denies the action, and the expected count of 5 only works if that slot counts the record as evidenced. So the slot measures reconstructibility, not favourability. This run counted it that way. The protocol never says so, and an implementer who counted a denying record as not evidencing authority would score H06 as 4 and still be reasoning defensibly from the text.

Third, the protocol gives no counting rule for conflicting, partial or unverifiable evidence. No case supplies two contradictory authority versions for the same interval. No case supplies an acceptance without an acknowledgement, or acknowledgements from both the designated role and a wrong role. No case states whose assertion makes a receipt evidenced: this run counted a receipt event in the record as evidenced receipt, which means the issuer's own record is taken at face value. A measure meant for audit use needs a stated rule for each of those, because that is where two honest assessors will diverge.

## Question 3: Interoperability

Could two independently developed implementations apply these requirements consistently?

This run is direct evidence that the core can be done. A second implementation, built from the text with no access to the author's code and no shared internal model, applied shared reference and resolution rules and reached the same outcome and the same count on all eight cases. The interval rule for action-time scope, valid_from at or before the action instant and valid_until after it, is stated mechanically and worked as stated.

Consistency beyond this run is not yet secured, because the following must be specified before two implementations can be expected to agree on records neither has seen:

1. A reference format. Record identifier, issuing platform, designated escalation role, scope version at issue, policy version at issue, duty class at issue and resolution endpoint. This run invented a minimal shape and recorded it in run-report.md. Any other shape is equally compatible with the current text.
2. Fetch and result semantics that distinguish the H05 situation from the H07 situation, so the two outcomes do not depend on an implementation's private record design.
3. The full outcome token set, including a token for the positive case, and a priority order when more than one token applies.
4. Slot counting rules for a denying authority record, for conflicting evidence and for assertions that cannot be verified from the record.
5. An evaluation instant for time-relative outcomes. H04 has none, and RECEIVED_NO_DESIGNATED_ACK is only true as of some instant. The protocol must say which.
6. Whether administrative events need timestamp proofs. The protocol is silent. This run used plain instants in the record.

## Protocol gaps, tied to cases

- G1, H01. No outcome token for the positive case. The expected observation is prose only.
- G2, H05 and H07. No specified way for a receiver to distinguish an unavailable historical reference from a returned current version. The two outcomes rest on an undefined fetch semantic.
- G3, H06. Slot 1 counting rule unstated. A denying authority record must count as evidenced to reach the expected 5, and the text does not say that.
- G4, H04. No test-end or evaluation instant. An unanswered escalation outcome is time-relative and the protocol fixes no time.
- G5, H06 with H03. No priority order among outcome tokens when a record satisfies more than one.
- G6, H03 and H08. No counting rule for conflicting or partial evidence: acceptance without acknowledgement, acknowledgement from both roles, or two versions claiming the same interval. No case exercises any of these.
- G7, all cases. No reference format, no resolution steps, no duty class pinned at issuance and no timestamp proofs on administrative events. Each absence forced a design choice in this run. The choices are recorded in run-report.md.
- G8, all cases. No field distinguishes revocation from narrowing to nothing. This run added a change_type field of its own. H01 and H06 turn on exactly that distinction, so the protocol's two central cases depend on a field the protocol does not define.
- G9, measurability. The six slots are defined in no artefact outside this protocol. The nearest published measure, in the W3C conformance format, has five different slots.
- G10, method. The protocol reports that the author's internal run used four mutation controls, but the controls are not specified in the text, so an independent run cannot reproduce that part of the method. None were invented here.

## Deltas against the owner's draft, logged and not merged

The task owner has a protocol draft of his own covering the same eight situations. This run scored the author's version, the author's way. The deltas were logged, not resolved.

1. Numbering and naming. The author numbers cases H01 to H08 with outcome tokens for most. The owner's draft numbers Cases 1 to 8 and states pass conditions in prose.
2. Case 1 and H01. The owner's Case 1 covers authority narrowed or revoked after the action, with no referral events. H01 is revocation only and bundles the full positive referral chain into the same case.
3. Case 4 and H04. The owner's Case 4 is an unanswered escalation evaluated at a stated test-end instant, with receipt not specified. H04 presupposes evidenced receipt and names no test-end instant. See G4.
4. Case 5 split. The owner's Case 5 is one case. The author splits it into H05 and H07, which score the authority conclusion differently. See G2.
5. Case 6 and H06. The owner's Case 6 anchors at the referral instant. H06 anchors at action time. This run applied the action-time anchor.
6. Completeness measure. The author uses one fixed denominator of six for every case and no separate pass or fail. The owner's draft scores completeness per case against that case's own setup events and reports an explicit pass or fail beside it. This run used the fixed denominator and no pass or fail, as instructed.
7. Missing apparatus. The author's text carries no reference format, no resolution steps, no duty class, no revocation versus narrowing field and no timestamp proofs. The owner's draft carries all of these. See G7 and G8.
8. Mutation controls. The author's internal run used four. The owner's draft carries none. The controls are not specified in the author's text, so they could not be reproduced here. See G10.
9. Interval rule. The author states the action-time interval rule mechanically. The owner's draft states decision-time version in prose. This run applied the mechanical rule.

## What this run does not establish

It does not establish that the expected outcomes are the correct expectations for a production hiring audit. The cases are synthetic and were authored by the same process that wrote the standard behind them. It does not establish conformance of any implementation to RI-STD-01. It does not establish that a second implementation would agree on unseen records, for the reasons in the interoperability answer. It establishes one narrower thing, and establishes it cleanly: the protocol as written can be implemented independently, its frozen outcomes can be reproduced from the record alone, and its gaps are the ten items listed above rather than matters of implementation taste.
