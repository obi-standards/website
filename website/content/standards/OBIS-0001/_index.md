---
title: "OBIS-0001: OBIS Document Lifecycle"
type: docs
weight: 1
bookToc: true
status: "Draft"
date: "2026-05-19"
editor: "Bernhard Haslhofer"
focus_area: "Process"
discussions-to: "https://github.com/obi-standards/website/discussions/TBD"
---

# OBIS-0001: OBIS Document Lifecycle

{{< status state="Draft" date="2026-05-19" editor="Bernhard Haslhofer" focus="Process" >}}

## Abstract

This document defines the lifecycle of OBIS standards documents: their states, the transitions between them, the rules governing identifiers and versioning, and the roles of editors, working group chairs, and contributors. It applies to itself.

## 1. Introduction

OBIS standards are published as numbered documents under the identifier scheme `OBIS-NNNN`. Each document progresses through a defined sequence of states, from initial drafting to publication, and may be later superseded or withdrawn. This document specifies that sequence and the conditions for moving between states.

The lifecycle is intentionally lightweight. It is modelled on IETF [RFC 2026](https://www.rfc-editor.org/rfc/rfc2026) and the [W3C Process Document](https://www.w3.org/policies/process/), and informed by the Bitcoin [BIP-2](https://github.com/bitcoin/bips/blob/master/bip-0002.mediawiki) and Ethereum [EIP-1](https://eips.ethereum.org/EIPS/eip-1) processes that have run similar work in crypto-native communities for over a decade. The result is reduced to what is necessary for a small, public, openly-developed body of work.

## 2. States

A document is at any time in exactly one of the following states.

- **Draft.** Under active development. Content, structure, and scope may change without notice. No stability commitments.
- **Public Review.** Content is frozen for a defined window during which the public is invited to submit comments. The default window is **30 days**.
- **Published.** The document has completed Public Review, substantive comments have been responded to per §3.2, and the editor and (when present) the working group chair have signed off. The content and identifier are stable.
- **Superseded.** A later Published document has replaced this one, recorded in the `superseded-by` preamble field (§4). The superseded document remains accessible at its URL.
- **Withdrawn.** The document has been retired without replacement. A retention notice with the reason remains at its URL.

## 3. State transitions

All documents, in every state, live on the `main` branch of the source repository (§9); the public site is built from `main`, so the current state of every document, including Drafts, is always visible. Contributors propose changes to a Draft as pull requests against `main`. A document enters the lifecycle when the editors merge a creation pull request titled `Draft: OBIS-NNNN` that adds the document in the Draft state; merging it assigns the next free identifier (§4). Every subsequent state transition is itself a pull request that changes only the document's status block and front matter (the Withdrawn transition additionally replaces the body with a retention notice, §3.5); the transition takes effect when that pull request is merged.

### 3.1 Draft → Public Review

The editor opens a pull request titled `Public Review: OBIS-NNNN` that changes the document's state to Public Review. The PR description records:

- the commit at which the content is frozen,
- the start and end dates of the comment window,
- the URL declared in the document's `discussions-to` preamble field, which is the canonical venue for comments during the review window.

Merging the pull request starts the comment window. While the window is open, no pull requests altering the document's content are merged; this constitutes the content freeze defined in §2. The transition is announced on the OBIS site and in any active community channels at the start of the window.

### 3.2 Public Review → Published

After the comment window closes:

1. The editor responds publicly to each substantive comment received (a comment asserting a technical or normative defect, as distinct from an editorial remark), indicating whether the comment was accepted, declined with rationale, or deferred.
2. Changes resulting from accepted comments are merged as ordinary pull requests.
3. The editor opens a pull request titled `Publish: OBIS-NNNN` that changes the state to Published. The editor and, when one exists, the working group chair (§8) sign off via approval of this pull request; in solo-editor mode (§3.3) the editor's approval alone completes publication.

When the publication pull request is merged, the merge commit is tagged `OBIS-NNNN-<publication date>` in git; the tag pins the citable text of the Published release.

### 3.3 Solo-editor mode (transitional)

This provision is transitional. It exists to enable an early body of published work to accumulate during the founding period, before working groups have formed around individual proposals.

Until a working group has formed around a proposal, the editor publishes after the 30-day Public Review window followed by a 7-day no-objection period announced at the close of review. The no-objection period gives any party identifying a substantive late objection a final opportunity to record it; a substantive objection recorded in this period suspends publication until the editor has responded per §3.2.

This mode is removed for a proposal as soon as its working group is in place, and the provision as a whole is intended to be retired once the project's contributor base supports working-group formation as the default path for new work. Removal of this section will itself follow the lifecycle defined in this document.

### 3.4 Published → Superseded

A Published document is superseded when a successor document declaring `replaces: OBIS-NNNN` in its preamble reaches Published. Upon the successor's publication, the successor's editor opens a transition pull request against the superseded document that sets its `superseded-by` field and changes its status badge to Superseded, linking to the successor. The superseded document remains accessible at its URL.

### 3.5 → Withdrawn

The editor may withdraw a document in any state except Superseded, with documented reason. The original URL is retained and serves a Withdrawn notice in place of the body.

## 4. Identifiers

Every OBIS document carries a permanent four-digit identifier of the form `OBIS-NNNN`, assigned by the editors in submission order at the time the document first enters the Draft state. Identifiers are never reused.

The identifier is independent of the document's title and focus area; renaming or re-scoping a document does not change its identifier.

Documents record relationships between identifiers in two preamble fields, following BIP-2: `replaces` names the document(s) a proposal supersedes; `superseded-by` is set on a Published document when its replacement reaches Published (§3.4).

## 5. Revisions

OBIS documents carry no version numbers. The document at its URL is the current text; the git history of the source path (§9) is the complete editorial record, and the tag created at publication (§3.2) pins the text that completed Public Review.

After publication, only editorial corrections that do not alter normative content (typographical fixes, dead-link repair, formatting) may be merged. Any change to the normative content of a Published document requires a new document under a new identifier, which declares `replaces: OBIS-NNNN` in its preamble and enters the lifecycle at Draft. Changes made in response to Public Review comments (§3.2) are pre-publication revisions and require no special handling.

Process documents, this document among them, are exempt: their function requires a stable identifier across amendments, so they re-enter the lifecycle at Draft under the same identifier (§10).

## 6. URLs

Every document has a single canonical URL: `https://obistandards.org/standards/OBIS-NNNN/`. It always serves the document in its current state, with the status block indicating that state. The text of each Published release is pinned by its publication tag (§3.2); all historical states are accessible through the git history of the source path (§9).

## 7. Required document structure

Every OBIS document MUST contain, in order:

1. A title of the form `OBIS-NNNN: <name>`.
2. A one-line status block: state, date, editor.
3. An abstract of one paragraph.
4. A numbered normative body.
5. A references section.

Every OBIS document MUST also carry a `discussions-to` field in its front-matter, pointing at a single GitHub Discussion thread that serves as the canonical venue for public comments on the document. The thread MUST exist at the latest when the document enters Public Review (§3.1); while in Draft, the field MAY carry a placeholder. This convention is borrowed from the Ethereum [EIP-1](https://eips.ethereum.org/EIPS/eip-1) preamble.

Documents MAY contain additional appendices, examples, and non-normative discussion. Normative content uses the keywords MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY in the sense of [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

## 8. Roles

- **Editor.** Shepherds the document through its states, integrates contributions, and is responsible for the public response to Public Review comments. During the founding period, drafts are edited by Bernhard Haslhofer; co-editors and named external reviewers are being recruited for each draft, and editorship transfers to a working group chair when a working group forms around a proposal.
- **Working group.** A self-organised set of contributors who form to develop a specific proposal (e.g., OBIS-0001) through the lifecycle. A working group is informal: it has no chartered membership and constitutes itself when work on the proposal begins. It dissolves when the proposal reaches Published or Withdrawn.
- **Working group chair.** Acts as a single point of accountability for a working group. Co-signs publication of the document and resolves disputes between contributors. The role is filled (or left vacant) by the working group itself; there is no external appointment.
- **Contributor.** Any individual proposing edits via pull request on the source repository. No membership or credential is required.

## 9. Source of truth

OBIS documents are authored in Markdown in the `obi-standards/website` repository under `website/content/standards/OBIS-NNNN/`. The git history of that path is the document's editorial history. Documents in all lifecycle states reside on `main`; there are no long-lived draft branches. The rendered HTML at `obistandards.org` is derived; in the event of a discrepancy, the source repository prevails.

## 10. Amendments to this document

This document is itself `OBIS-0001` and progresses through the lifecycle it defines. As a process document it retains its identifier across amendments (§5): substantive amendments re-enter the lifecycle at Draft under the same identifier and republish per §3. The tag created at each publication (§3.2) preserves the text of every prior release.

## References

- IETF [RFC 2026](https://www.rfc-editor.org/rfc/rfc2026), *The Internet Standards Process, Revision 3*.
- IETF [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119), *Key words for use in RFCs to Indicate Requirement Levels*.
- W3C, [*W3C Process Document*](https://www.w3.org/policies/process/).
- Bitcoin, [BIP-2](https://github.com/bitcoin/bips/blob/master/bip-0002.mediawiki), *BIP process, revised*.
- Ethereum, [EIP-1](https://eips.ethereum.org/EIPS/eip-1), *EIP Purpose and Guidelines*.
