---
title: "OBIS-0002: Shared Taxonomies for Blockchain Intelligence"
type: docs
weight: 2
bookToc: true
status: "Draft"
date: "2026-05-19"
editor: "Bernhard Haslhofer"
focus_area: "Terminology"
discussions-to: "https://github.com/obi-standards/website/discussions/TBD"
---

# OBIS-0002: Shared Taxonomies for Blockchain Intelligence

{{< status state="Draft" date="2026-05-19" editor="Bernhard Haslhofer" focus="Terminology" >}}

## Abstract

Blockchain intelligence tools label addresses, services, and events with categorical information, but each platform maintains its own vocabulary: identical concepts carry different names, and labels produced in one ecosystem cannot be reliably interpreted in another. This document aims to establish a shared classification baseline that independent implementations can reference without giving up their internal vocabularies. It defines shared taxonomies for blockchain intelligence as two concept schemes, Actor Type and Abuse Type, each anchored by a small set of precisely defined top concepts. Refinement happens beneath the top concepts, through narrower concepts and vendor-specific extensions, rather than through growth at the top level.

## 1. Introduction

Most work in blockchain intelligence requires labelling addresses, services, and events with categorical information. What kind of service is this (e.g., centralised exchange, mixer, DEX)? What kind of abuse has been observed (e.g., ransomware, scam, sextortion)? Different communities have produced different vocabularies in response to similar questions, and tools that interoperate across communities have to map between them.

OBIS-0002 commits to a set of shared concept schemes, owned and maintained openly, that downstream OBIS specifications can reference. The initial release covers actor type and abuse type, in each case through a small number of precisely defined top concepts.

This document deliberately specifies only high-level concepts. Interoperable exchange requires agreement at the top of the hierarchy, not uniformity at the bottom: implementations refine the shared top concepts through narrower, vendor-specific extension concepts (§7), and refinements that prove broadly useful are promoted into the shared schemes by revision.

## 2. Scope

This document specifies two concept schemes:

- **Actor type.** What kind of real-world participant an address represents (§5).
- **Abuse type.** What kind of harmful activity has been observed (§6).

Further classification dimensions are out of scope for this release; deferrals are recorded in §9.

## 3. Terminology

The key words **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

Structural terminology follows the W3C [Simple Knowledge Organization System (SKOS)](https://www.w3.org/TR/skos-reference/) vocabulary; where this document says *concept*, *concept scheme*, *broader*, or *narrower*, the terms carry their SKOS meaning.

- **Concept.** A single unit of meaning in an OBIS concept scheme, carrying a stable identifier, a normative definition, and labels.
- **Concept scheme.** A coherent set of concepts covering one classification dimension (e.g., the OBIS Actor Type scheme).
- **Top concept.** A concept that anchors a scheme. Every other concept in the scheme is narrower than exactly one top concept.
- **Broader / narrower.** The hierarchical relations between concepts. A narrower concept refines its broader concept and is identified with the dot-separated form `<top>.<specific>`.
- **Label.** A human-readable, language-tagged name for a concept (SKOS preferred label). Labels may evolve; identifiers do not.
- **Source taxonomy.** A pre-existing taxonomy that OBIS concepts map to (e.g., INTERPOL Entity Taxonomy).

## 4. Design principles

OBIS-0002 commits to the following principles, derived from the dimensions on which existing efforts vary (§8):

1. **Small top level, expandable in depth.** Each scheme defines a handful of top concepts; specificity is added by narrower concepts rather than by widening the top level.
2. **Hierarchical identifiers.** Narrower concepts are identified `<top>.<specific>` (e.g., `service.exchange`). Implementations MAY use the top-concept identifier alone when the narrower concept is unknown or unnecessary.
3. **Stable identifiers.** Identifiers do not change with rewording; labels and definitions may evolve, but the identifier is permanent.
4. **Language-tagged labels.** Identifiers are language-neutral; each concept carries one preferred label per language (e.g., `service.exchange` with the labels "Cryptoasset Exchange" (en) and "Kryptowährungsbörse" (de)). Definitions are normative in English.
5. **Open extension.** Implementations MAY introduce extension concepts with the `x-` prefix on the specific segment (e.g., `service.x-bespoke`); OBIS reserves all non-`x-` identifiers (§7).
6. **Explicit mapping to source taxonomies.** Mappings to INTERPOL and other source taxonomies are maintained separately from the concept tables, keeping the schemes self-contained; the initial mappings are deferred (§9).
7. **Conservative additions.** The initial schemes are small and cover the cases most frequently exchanged in practice. Coverage grows by revision through the document lifecycle, not by ad hoc per-implementation additions.

## 5. Actor Type concept scheme

Actor typing answers one recurring question: is an address an intermediary holding assets for others, or an endpoint of control in itself? Investigative tracing is in practice the pursuit of a path to a service subject to customer due-diligence obligations, which holds identifying records and can respond to legal process; a service address is therefore a potential attribution endpoint, a party address a terminus where attribution requires other evidence. The same distinction precedes counterparty categorisation for reporting entities and supervisors. Two concepts keep the top level typically assertable from on-chain evidence and stable across jurisdictions; contested distinctions are deferred (§9).

The Actor Type scheme is anchored by two top concepts, distinguished by the capacity in which control over an address is exercised. Every actor-type label SHOULD carry a top-concept identifier; narrower concepts are deferred (§9).

| Identifier | Definition |
|---|---|
| `service` | Control exercised in the course of providing a function to others: custody, exchange, payment, or infrastructure. |
| `party` | Control exercised by a real-world entity on its own behalf: a natural person or an organisation. |

## 6. Abuse Type concept scheme

Blockchain intelligence tools label addresses with the wrong they are associated with, but each vendor uses its own category names, so labels cannot be compared or exchanged between tools and agencies. The Abuse Type scheme provides a common set of top concepts for these labels. It classifies by the manner in which the holder authorised the transfer of value rather than by offence name, because offence names differ between jurisdictions while the underlying facts of the transfer do not.

The Abuse Type scheme is anchored by four top concepts, distinguished by whether and how the holder authorised the transfer of value. Every abuse-type label SHOULD carry a top-concept identifier; narrower concepts are deferred (§9).

| Identifier | Definition |
|---|---|
| `theft` | Value transferred without any authorisation by the holder (key compromise, contract exploit, transfers signed by an attacker with exfiltrated keys). |
| `fraud` | Value transferred with the holder's authorisation, procured by deception (investment scams, rug pulls, approval phishing where the holder signs a deceptively procured transaction). |
| `extortion` | Value transferred with the holder's authorisation, procured by threat or coercion (ransomware, sextortion). |
| `illicit-finance` | Payment in furtherance of activity unlawful in itself, absent a holder deprived of value against their will (trade in prohibited goods and content including CSAM, sanctions evasion, terrorism financing). |

Implementations using concepts from either scheme in OBIS-0003 records (or any other OBIS context) MUST use the OBIS identifier on exchange. They MAY retain alternative internal representations.

Records labelling activity that involves CSAM or terrorism financing under `illicit-finance` carry elevated handling obligations; see [OBIS-0003]({{< relref "OBIS-0003" >}}) §8 (privacy and security).

## 7. Extension mechanism

Implementations MAY introduce extension concepts narrower than the top concepts defined in §5 and §6, subject to the following rules:

- Extension concepts MUST carry the `x-` prefix on the specific segment (e.g., `service.x-bespoke`, `fraud.x-trade-finance`).
- Extension concepts MUST be defined in documentation accessible to the receiving party (e.g., an external schema document).
- Recipients of records containing extension concepts MUST treat unknown extensions as opaque labels under their declared top concept, rather than ignoring the label entirely.
- Extension concepts with broad utility SHOULD be proposed for promotion to a non-prefixed OBIS narrower concept in a future revision of this document.

## 8. Related work

### 8.1 INTERPOL Darkweb and Virtual Assets Taxonomy

The [INTERPOL Innovation Centre](https://interpol-innovation-centre.github.io/DW-VA-Taxonomy/), via its Darknet and Cryptocurrencies Working Group, publishes two coordinated taxonomies:

- **Entity Taxonomy** (v0.3): real-world actors and services in dark-web and cryptoasset ecosystems.
- **Abuse Taxonomy** (v0.1): forms of improper service deployment or abuse.

Both are published in human-readable form alongside machine-readable downloads (CSV), are developed on a public Git repository, and explicitly "build on existing definitions and do not claim to replace them." They are maintained by an INTERPOL working group composed of law-enforcement and academic contributors; latest revision 2022. The INTERPOL taxonomies are the de facto base used by open-source investigations tooling and the most direct prior art for OBIS-0002.

### 8.2 GraphSense conventions

GraphSense [TagPacks](https://github.com/graphsense/graphsense-tagpacks/wiki/GraphSense-TagPacks) reuse the INTERPOL Entity and Abuse taxonomies as their `category` and `abuse` fields rather than maintaining a separate vocabulary. The choice is significant: an investigations-focused open-source tooling ecosystem treats the INTERPOL taxonomy as the operational base.

### 8.3 Closed commercial classifications

The major commercial blockchain analytics vendors (e.g., Chainalysis, TRM Labs, Elliptic) each maintain proprietary actor and abuse taxonomies. These are not publicly redistributable and frequently differ in granularity and terminology, both from one another and from INTERPOL. They are noted because tooling that interoperates with these vendors must in practice map to and from them; they cannot serve as the basis for an open standard.

## 9. Open issues

- **Narrower concepts.** This release defines top concepts only. Shared narrower concepts (e.g., `service.exchange`, `extortion.ransomware`) and distinctions contested at the top level (e.g., custodial vs non-custodial services, autonomous code acting as a service) are deferred to a future revision; until then, refinement happens through the extension mechanism (§7).
- **Source-taxonomy mappings.** Mappings to the INTERPOL Entity and Abuse taxonomies, together with a mapping-relation notation, are deferred to a future revision.
- **Protocol-category scheme.** A classification of DeFi protocol roles (e.g., DEX, lending, liquid staking) is deferred; the community-curated [DefiLlama categories](https://defillama.com/categories) are the expected starting base.
- **Serialization.** A machine-readable serialization of the concept schemes, covering both the standardised OBIS concepts and vendor-specific extension concepts (e.g., as SKOS/RDF or JSON), is deferred; until then, the tables in this document are the normative representation.
- **Multi-classification.** Whether a single address may carry more than one concept from the same scheme is left to the data format ([OBIS-0003]({{< relref "OBIS-0003" >}})) and is not constrained by this document.

## References

- IETF [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119), *Key words for use in RFCs to Indicate Requirement Levels*.
- W3C, [*SKOS Simple Knowledge Organization System Reference*](https://www.w3.org/TR/skos-reference/), W3C Recommendation, 18 August 2009.
- INTERPOL Innovation Centre, [*Darkweb and Virtual Assets Taxonomy*](https://interpol-innovation-centre.github.io/DW-VA-Taxonomy/). Entity Taxonomy v0.3, Abuse Taxonomy v0.1.
- DefiLlama, [*Protocol Categories*](https://defillama.com/categories).
- GraphSense, [*TagPacks Wiki*](https://github.com/graphsense/graphsense-tagpacks/wiki/GraphSense-TagPacks).
- [OBIS-0001]({{< relref "OBIS-0001" >}}), *OBIS Document Lifecycle*.
- [OBIS-0003]({{< relref "OBIS-0003" >}}), *Attribution Tag Data Model and Exchange Format*.
