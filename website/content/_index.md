---
title: Open Blockchain Intelligence Standards
type: docs
bookToc: false
---

<section class="obis-hero">
  <h1 class="obis-title">Open Blockchain Intelligence Standards</h1>
  <p class="obis-tagline">A bottom-up community effort to develop open standards for blockchain intelligence.</p>
</section>

Blockchain intelligence is transitioning from an emerging field into an established professional domain, used by investigators, prosecutors, supervisors, and researchers in high-stakes settings (e.g., criminal proceedings, supervisory enforcement, peer-reviewed research). The infrastructure that domain depends on has not made the same transition. Data formats vary between platforms, identical concepts carry different names, foundational computations follow divergent approaches, and findings produced in one ecosystem are difficult to verify or reuse in another.

OBIS develops open, vendor-neutral specifications to close that gap, in public, with anyone who wants to contribute.

## About {#about}

OBIS is a community effort. Drafts are developed in the open on GitHub. The process is modelled on the IETF and W3C (public drafts, defined review cycles, no membership tiers, no certification business), but the organisational form is intentionally light: there is no board, no chartered membership, and no application to join. OBIS organises standards around **concrete use cases**, because the gaps that matter most appear at the boundary between organisations doing similar work with incompatible tools.

OBIS is currently an unincorporated open community project. Incorporation as a non-profit standards organisation is planned and will be undertaken once the early body of work and contributor base warrant it. Until then, the project operates without legal personhood: contributions are made directly to the public specifications under the licenses described on the [License](/about/license/) page, and the project holds no funds, assets, or contractual obligations.

At its core, OBIS is a body of open specifications, developed in public by whoever is willing to contribute.

Researchers and practitioners articulated the motivation for this work in detail at the [9th Global Conference on Criminal Finances and Cryptoassets](https://baselgovernance.org/blog/developing-blockchain-intelligence-standards-and-interoperability-critical-need-fight) and elsewhere in the field. OBIS is now the venue for turning that motivation into specifications.

## Focus areas {#focus-areas}

Three use-case domains anchor the first work cycle. Each is grounded in a concrete, documented interoperability problem.

<div class="obis-focus-grid">

{{< obis-card mark="§ I" title="Investigations, forensics, and attribution" >}}

Investigators today work in isolated tool ecosystems with no systematic mechanism to share findings and investigation leads across platforms or agencies. Prosecutors struggle to demonstrate the reliability, admissibility, and validity of blockchain evidence in court because no standardised validation procedures exist. As a consequence, judges must rely on case-by-case testimony from individual tool providers.

OBIS work in this area: shared [terminologies and taxonomies]({{< relref "/standards/OBIS-0002" >}}), data models and exchange formats for [address attribution]({{< relref "/standards/OBIS-0003" >}}), and reference implementations for address clustering, including formats that allow transaction-graph sharing across organisations without exposing proprietary attribution data.
{{< /obis-card >}}

{{< obis-card mark="§ II" title="Regulatory reporting and supervision" >}}

Supervisors apply inconsistent methodologies and typologies when assessing virtual-asset activity, and reporting entities maintain bespoke integrations with each supervisor and counterparty they exchange data with.

OBIS work in this area: standardised exchange formats between cryptoasset service providers (CASPs), supervisors, and adjacent reporting entities, reducing bespoke integration cost and improving the comparability of supervisory data across jurisdictions.
{{< /obis-card >}}

{{< obis-card mark="§ III" title="Open analytics and research data" >}}

Academic and applied research on blockchain data is held back by the absence of shared data sets, schemas, labelling conventions, and reproducibility primitives. Each new study re-derives its data layer from raw chain history.

OBIS work in this area: schemas and conventions that let research compound across studies, building cumulative science on top of blockchain data.
{{< /obis-card >}}

</div>

A fourth area, compliance and sanctions screening, is intentionally **out of scope at launch**. That space is densely commercial and well-served by existing vendor formats.

## Relationship to existing work {#relationship-to-existing-work}

OBIS specifications are designed to sit alongside the existing body of work in this space. Several instruments and reference works define the field that OBIS specifications operate within:

- **FATF Recommendations and guidance**, in particular Recommendation 15 on virtual assets and Recommendation 16 on the Travel Rule, set the international policy framework. OBIS produces technical artefacts that implementations of policy can build on, without producing policy or interpreting FATF guidance itself.
- **EU instruments** including MiCA (Regulation (EU) 2023/1114), the recast Transfer of Funds Regulation, and EBA reporting frameworks define obligations and reporting expectations for entities operating in the EU. OBIS specifications in the regulatory-reporting focus area are intended to be compatible with these obligations and to reduce the integration cost of meeting them, without replacing or reinterpreting them.
- **IVMS101** is the established data standard for originator and beneficiary identity information accompanying VASP-to-VASP transfers. It carries identity information disclosed by counterparties at transfer time. OBIS attribution work (e.g., OBIS-0003) operates on a different segment of the workflow and does not subsume IVMS101.
- **INTERPOL DW-VA-Taxonomy** is a widely-referenced taxonomy for darkweb and virtual-asset activity. OBIS taxonomies in this area draw on it as prior art and aim to remain compatible where the underlying concepts overlap.
- **National supervisory frameworks** vary by jurisdiction. OBIS specifications are designed to be referenceable by supervisors that choose to adopt them, without prescribing adoption.

The leverage of OBIS lies in the technical layer beneath all of the above, where the absence of shared formats and vocabularies currently imposes a cost on every party operating across organisational and jurisdictional boundaries.

## Process {#process}

OBIS documents progress through three states: **Draft**, **Public Review**, and **Published**. Drafts are developed in the open on GitHub. A draft reaches Public Review only after rough consensus has emerged among contributors, and reaches Published only after a public comment period has closed and substantive objections have been addressed.

The full process is specified in [OBIS-0001: OBIS Document Lifecycle](/standards/obis-0001/), currently in Draft.

## Get involved {#get-involved}

OBIS is developed in the open. Anyone interested in the work is welcome to follow it, comment on drafts, or contribute.

- **Drafts and discussion:** [github.com/obi-standards](https://github.com/obi-standards). Public development of all specifications. Anyone with a GitHub account can open issues, comment on drafts, and submit pull requests. No application or membership is required.
- **Email:** <info@obistandards.org>. General correspondence about the project.
- **Written commentary on drafts (institutional channel):** Institutions that prefer not to engage via GitHub (supervisory bodies, FIUs, government agencies, and other organisations whose internal processes do not accommodate public pull-request workflows) may submit written commentary on any current draft or document in Public Review by emailing <info@obistandards.org> with the subject line `Commentary: OBIS-NNNN`. Commentary received this way is treated equivalently to commentary received via GitHub: it is acknowledged publicly, considered in the editor's response, and recorded as part of the review record. Senders may request that the institutional affiliation be recorded without naming the individual signatory.

### Why participate

OBIS is open to anyone interested in the work. Different kinds of organisations and individuals have different reasons to engage, and different forms of engagement that suit them. The following framings describe how each audience typically relates to the work.

**Tool providers (blockchain analytics platforms, forensic tooling, on-chain data vendors).** OBIS specifications reduce the per-customer integration cost of supporting cross-organisation exchange. Vendors retain proprietary value in the data, attribution methods, and analytical capabilities they produce, while OBIS standardises only the interchange formats and shared vocabularies between organisations. Participation lets a vendor influence the shape of those interfaces, surface implementation constraints early, and document interoperability claims their procurement counterparties increasingly ask about. OBIS does not certify implementations, accredit vendors, or operate any process that ranks participating vendors against non-participating ones.

**Authorities (supervisors, financial intelligence units, prosecutors, central-bank analytics units, law-enforcement bodies).** OBIS specifications aim to make supervisory data more comparable across jurisdictions, reduce the bespoke-integration burden on reporting entities, and provide a shared technical baseline that prosecutors and courts can refer to when assessing the reliability of blockchain evidence. OBIS contributes the technical artefacts that implementations of regulation and guidance can build on, and leaves the regulation and guidance themselves to the bodies with a mandate for them. Authorities can engage as observers, as commenters on drafts in Public Review, or as co-editors and reviewers where their institution's mandate permits.

**Researchers (academic and applied).** OBIS specifications provide shared schemas, vocabularies, and reproducibility primitives that let work compound across studies without re-deriving its data layer from raw chain history each time. Participation is valuable both as a contributor (proposing or co-editing specifications that codify what the field already knows) and as a user (citing OBIS specifications in methods sections, allowing other groups to reproduce and extend results). Research outputs that depend on specific attribution data, taxonomies, or data layers are particularly well-served by being expressed in terms of an open specification.

**Reporting entities (CASPs, exchanges, custodians, payment institutions handling virtual assets).** OBIS specifications in the regulatory-reporting focus area aim to reduce the cost of maintaining bespoke integrations with each supervisor and counterparty. Reporting entities have direct visibility into where bespoke-integration cost actually falls, which makes their input on draft exchange formats especially valuable. Engagement is technical input into the design of formats that the entity may or may not eventually adopt, and carries no regulatory commitment.

### Co-editors and external reviewers

The current OBIS drafts are edited by a single founding editor. This reflects the project's early stage. OBIS is actively seeking co-editors and named external reviewers for each draft, particularly from organisations and jurisdictions not yet represented in the contributor base.

If you have relevant expertise (practitioner experience in investigations, supervisory or prosecutorial work, research on blockchain data, or implementation experience with blockchain analytics tooling) and are interested in serving as a co-editor or named reviewer on one of the current drafts, please open an issue on the relevant repository or write to <info@obistandards.org>.
