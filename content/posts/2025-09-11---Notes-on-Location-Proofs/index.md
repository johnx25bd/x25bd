---
title: "Notes on Location Proofs"
date: "2025-09-11T12:00:00.000Z"
template: "post"
draft: false
slug: "/posts/notes-on-location-proofs"
category: "Web3"
tags:
  - "Location Proofs"
  - "Web3"
  - "Geospatial"
description: "An exploration of proof-of-location systems, their technical implementations, privacy implications, and potential applications in Web3 and beyond."
socialImage: "./media/dutch-boats.png"
---

For the past seven years, I’ve been returning again and again to a set of questions I can’t put out of my mind. In a nutshell: how can **geospatial technologies** be enhanced or improved by **Web3 tools and design principles**? And conversely, how can we integrate geospatial computing capabilities into decentralized systems like Ethereum and IPFS?


> **Note:** The first section of this post will go over the background and motivation — if you're pressed for time, [jump ahead to Proof Of Location Systems](#proof-of-location-systems).

Crypto isn’t my home turf. I’ve been working professionally with geospatial data for my entire career:

- 2009 — satellite imagery analysis in my undergrad
- 2012 — co-founder at Junctions, a location-based app startup;
- 2017 — geospatial data science of shipping patterns; 
- 2019 — MSc in Spatial Data Science and Visualisation at UCL
- 2021 — a formative spell at Ordnance Survey, the UK’s national mapping agency. 

Ever since I discovered Ethereum in 2017, and came to recognize the importance of [Web3 design principles](https://www.x25bd.com/posts/web3-design-principles) — open, durable, and opt-in — I couldn’t help but wonder how geospatial data could fit into this new paradigm.

---

### Motivation

When I first delved into blockchains I was working as a geospatial data scientist / product developer at an international NGO studying peace and security issues, focused on maritime security. I wrote an internal memo about how North Korea evades international sanctions, exporting coal to foreign markets to fund their nuclear weapons program. 

I wasn’t surprised by the shell companies or reflagging schemes. What did surprise me was a technical tactic: ships would sail to a particular offshore location, switch off their AIS transceivers, steam into port, load up, then reappear on the map days later. (AIS is the [Automatic Identification System](https://shipping.nato.int/nsc/operations/news/2021/ais-automatic-identification-system-overview), mandated by the UN’s International Maritime Organization, requires commercial vessels to broadcast their identity and location for safety and monitoring.)

I was a few months into crypto at that point, awash in buzzwords like “verifiability” and “censorship resistance.” Seeing how the ability to lie by omission was encoded into international shipping rules planted a seed: how could we do better than this? My masters at the Bartlett only reinforced my intuition: in a future of autonomous machines, strong and useful ways to represent *where* devices were in space would be important.

### Astral

Over the years those seeds have germinated and sprouted into the project I now lead, [Astral](https://www.astral.global/). Since leaving [Toucan](https://toucan.earth/), a startup I co-founded to improve access and accountability in carbon markets (which depend heavily on geospatial data) using blockchains and smart contracts, I’ve been working on Astral and collaborating with a team led by [Professor Taylor Oshan](https://geog.umd.edu/facultyprofile/oshan/taylor) at the University of Maryland, laying the groundwork for a decentralized geospatial web aligned with Web3 design principles. In April, we published a [paper](https://osf.io/bg2uq_v1) outlining the three pillars we see needed for this technology ecosystem to emerge.

One pillar — perhaps the most important one — focuses on **proof-of-location systems**. This post outlines a lot of our thinking about how credible claims about *where things happen* can be made online — an environment where trust is being eroded and generative AI is forcing us to question what’s real. 

My aim here isn't to provide all the answers — there are a lot of technical, social, regulatory, and commercial specifics that remain unexplored. Instead, I hope to sketch the contours of a field that feels increasingly important, to articulate my thinking and prompt discussion.

---

## **Everyday Examples of Location Evidence**

Before we get to definitions, it helps to notice how common location verification already is in daily life. Websites infer location by IP address — many services block access to users from different locations based on this data. Mobile apps grab geographic coordinates from smartphone GPS chips. NFC key cards unlock access to gyms and office buildings. Border officers check people into countries.

These are all ways of producing and assessing **location evidence** — practical mechanisms that give someone else some degree of confidence about where and when an event occurred.

## **Proof-of-Location Systems**

I use the term **proof-of-location system** to mean any system that produces evidence that supports a location claim. A location claim is a spatially referenced assertion about the position and, optionally, timing of anything – a person, device, asset, area, or event. 

Our initial research identified seven broad categories of sources of location evidence:

- **Authority**: Verified by a trusted person or institution (passport control, event admission).
- **Social**: Peers mutually verify presence (digital check-ins, vouching).
- **Near-field machine**: Devices confirm co-presence via Bluetooth, NFC, RFID.
- **Network machine**: Distributed nodes confirm via triangulation or time-of-flight.
- **Sensor data**: Photographic, acoustic, inertial, or environmental signals.
- **Delegated**: Piggybacking on existing trusted systems (bank statements, Uber rides, utility bills).
- **Legal**: Formal attestations in affidavits, bills of lading, customs documents, contracts etc.

This list is pragmatic, not exhaustive — the goal was to get a handle on how location is actually verified in practice.

## **From Systems to Proofs**

Each of the systems I just described — whether it’s a GPS chip, an NFC card reader, or a border officer stamping a passport — produces a piece of evidence about location. I’ve been calling these **location stamps**: discrete, verifiable signals — clues about where and when something happened.

On their own, stamps can be useful, but they’re limited. A GPS reading can be spoofed. An IP address can be manipulated with a VPN. A legal form can be falsified. Each stamp makes lying a little harder, but no single system is immune to manipulation.

The real strength comes when **multiple independent signals are combined** into a single artifact. That combination — bringing together evidence from different systems and checking how they align — produces what we call a **location proof**.

> A location proof is a verifiable digital artifact that supports a claim about the timing and location of an observed event, such that forging it would require collusion, technical manipulation, or fraud.
> 

The principle is straightforward:

- **Independent evidence strengthens the claim.** If one stamp can be forged, forging two or three unrelated ones together becomes much harder.
- **Correlated evidence adds little.** Stacking multiple GPS readings doesn’t help much; if one can be spoofed, the others can too.

So the distinction is:

- A *location stamp* is one piece of verifiable location evidence.
- A *location proof* is what you get when multiple stamps are combined and verified together.

This is why I think of proofs as lying on a **spectrum of certainty**, an idea I first encountered through [Kiersten Jowett’s work](https://figshare.unimelb.edu.au/articles/media/Proof_of_Location/13093577?file=25089257) at the University of Melbourne.

| **Level** | **Description** |
| --- | --- |
| 0 | A self-issued, digitally signed claim of location and time, with no external verification. |
| 1 | Augments a self-reported location claim with one piece of externally sourced evidence — one “weak” strategy. |
| 2 | Some evidence attached — one strong strategy, or 2–3 weak strategies. Some effort required to forge. |
| 3 | A proof that integrates multiple independent evidence sources (such as sensor data and network triangulation) to cross-verify the location. Maybe requires at least one “strong” strategy. |
| 4 | A proof that leverages diverse, high-integrity signals and strong cryptographic measures, making forgery significantly harder. |
| 5 | A proof designed to resist even nation-state level attacks, using advanced cryptographic protocols and multiple cross-domain endorsements. |

![A generalized multi-signal location proof workflow](media/location-proof.png)

### In Practice

To ground this in the original motivation — detecting maritime sanctions evasion — imagine how location proofs could change the picture.

Today, ships use AIS (Automatic Identification System) transceivers to broadcast their location. AIS is mandated by the UN’s International Maritime Organization to improve safety and monitoring of commercial vessels. But as I described earlier, even though they’re told not to (policy enforcement), ships can simply switch AIS off (no technical enforcement). That’s enough to move sanctioned cargo without sufficient scrutiny.

A location-proof approach would look different. Ships could be required to generate location proofs that draw on multiple independent systems:

- **Multi-constellation GNSS** (GPS, Galileo, GLONASS) to prevent reliance on a single satellite system.
- **Onboard sensor logs** (inertial data, engine activity, radar returns) to corroborate reported movement.
- **Proximity to known beacons** such as navigational markers or coastal infrastructure.
- **Legal attestation** signed by the ship’s captain or operator, raising the cost of lying through legal exposure.

Combined, these stamps would form a much stronger proof than AIS alone. Forging such a proof would require collusion across multiple systems, tampering with hardware, or coordinated fraud — far harder than just flipping a transceiver off. It wouldn’t make sanctions evasion impossible, but it would significantly raise the cost and lower the likelihood of going undetected.

A simpler use case: geoblocking website access. VPNs are consumer-grade technology, easy to use. Requiring users to provide additional independent signals corroborating their IP location improves the likelihood that they are where they claim to be, reducing fraudulent logins and enhancing compliance to location-based jurisdictional restrictions.

---

## **Why We’re Doing This**

This isn’t research for the sake of it. For a long time, I’ve been thinking through what we’d need to build location-based services fit for the decentralized web. In my deep dive into Ethereum and other decentralized systems, I saw that open, composable, cryptographically verifiable design patterns produced more reliable architectures, and guarded against arbitrary manipulation by malicious or compromised administrators.

I believe there’s a growing need for [public digital infrastructure](https://www.ucl.ac.uk/bartlett/publications/2024/mar/digital-public-infrastructure-and-public-value-what-public-about-dpi) built to serve humanity — a neutral base that resists capture by any special interests. This is true for finance, this is true for AI, and I believe this is true for location-based services.

We’re working toward a framework for location verification that could be relevant in trust-minimized contexts — especially those where incentives to lie about location are strong.

An in-depth defense of the need for this framework is beyond the scope of this post, but suffice to say:

- Location verification is a very common need online.
- Different use cases have different regulatory, user, commercial, and technical requirements.
- Right now it’s done either in weak ways (checking IP addresses, accepting GPS coordinates without corroboration), or as custom-built, inconsistent solutions.

The intuition here — grounded in many conversations and interviews — is that a coherent framework for verifying location in digital systems would improve trust, reduce costs, and open new opportunities.

## **Why This Matters Now**

Several converging trends make location proofs increasingly relevant:

1. **Web3 design.** On Ethereum, a transaction could be sent from Metamask, Zerion, Rabby, or any other wallet. Developers can’t assume what client produced it. Unlike Monzo — where transfers can only come from the Monzo app — Web3 transactions decouple identity from client software. If an app wants to rely on user location, the claim needs portable, verifiable evidence baked in.
2. **Web2 messiness.** In today’s Web2 environment, location is enforced through a mishmash of techniques: GeoIP lookups, GPS coordinates, billing addresses, app permissions, SLAs. These are inconsistent, hard to audit, and rarely portable across systems. A unified framework for signed location evidence could cut down on redundant checks and provide clearer audit trails.
3. **Regulation and compliance.** Many regulatory questions boil down to “where.” Data residency laws, KYC/AML requirements, and sanctions enforcement all depend on location. Current practice often relies on contracts and manual audits. Structured, portable proofs could lower overhead while improving auditability.
4. **Rising risk of misrepresentation.** Ships going dark on AIS. GPS spoofing. Deepfakes and AI-generated media. The cost of lying about where and when something happened has never been lower. Stronger, independently verifiable evidence raises the bar.
5. **[Splinternet](https://www.economist.com/business/2025/09/04/what-the-splinternet-means-for-big-tech) pressures.** The internet is global in theory, but it's governed locally. This is increasingly visible as different jurisdictions assert control: GDPR in Europe, MiCA for digital assets, national-level data residency rules. Multi-jurisdiction blockchain deployments make this especially acute. A consistent framework for verifiable location data would simplify compliance — especially as physical jurisdictions form [different rules governing AI systems](https://www.nytimes.com/2025/09/02/opinion/ai-us-china.html). 

---

## **Challenges + Open Terrain**

Plenty remains unresolved. I’ve been drawn to designing for an open innovation ecosystem, anticipating the value that can emerge when protocols are adopted at scale. This approach is rooted in designing and building instructive implementations — prototypes and POCs in transport, gaming, social, climate monitoring, etc. But there’s a lot to be learned through real-world deployment of location proofs.

Things I’m thinking about these days:

- **Hardware and sensor integrity.** Proofs are only as strong as the devices and sensors producing evidence. Trusted execution environments (TEEs), hardware signing, and sensor fusion help, but none are perfect defenses against tampering.
- **Privacy and user agency.** Location data is personally identifiable information (PII), regulated under frameworks like GDPR in Europe. Protecting it isn’t optional.
    - Selective disclosure and reduced granularity can limit exposure.
    - Collaborators of ours have implemented zero-knowledge point-in-polygon tests — useful for proving you’re inside a region without revealing exact coordinates. But GPS coordinates are just numbers: without corroborative evidence, that’s a zk proof of geometry, not of location. This is why PoL, not just cryptography, matters.
    - We’ve also explored TEE-based approaches.
    - This deserves more depth, but suffice to say: privacy is a core design principle.
- **Multi-signal weighting.** How do different PoL systems complement each other? How should evidence be weighted when stamps conflict or vary in strength?
- **User experience and adoption.** Proofs can’t create too much friction. If they do, they won’t be used.
- **Use cases.** Identity + authentication, blockchain intelligence, fraud + compliance, supply chain + logistics, consumer + social — all have different requirements for strength and usability.
- **Durability, not perfection.** The goal isn’t absolute certainty. It’s making lying harder, and ensuring that verification is consistent and transparent.

## **Current Work**

At the [University of Maryland](https://easierdata.org/), we’re cataloging existing verification strategies, developing frameworks for “stacked proofs,” and exploring privacy-preserving designs. This is ongoing, and we’re looking to speak with anyone who verifies location data for their company or use case.

In addition to this current work, through our role leading the Open Geospatial Consortium’s Blockchain and DLT Working Group (Prof Oshan is co-chair), we’re working on the [**Location Protocol](https://easierdata.org/updates/2025/2025-05-19-location-protocol-spec).** It’s a standardized schema for structuring, signing, and transporting location data — and a carrier for location proofs. I think of it as the envelope, not the evidence itself. It ensures verifiability, consistency, portability, and compatibility across systems.

The Location Protocol doesn’t replace commonly-used location data formats like existing formats like GeoJSON, GPX, GeoTIFF, etc. It complements them by wrapping these artifacts in standardized metadata required to interpret them, and by adding digital signatures. This makes location data portable, verifiable, and usable across decentralized and traditional systems alike. The reference implementation of the Location Protocol is built on the [Ethereum Attestation Service](https://attest.org/).

## **Future Directions**

Looking ahead:

- **Multi-source, composable location verification at scale.** Bringing together diverse signals into robust, reusable proofs.
- **Location-based services for smart contracts.** Verifiable geocomputation — checking containment, distance, length, area — introduces new tools for smart contract developers, like onchain geofencing.
- **AI analytics for anomaly detection.** Using pattern recognition to flag suspicious or inconsistent location evidence.
- **Machine-enforced compliance.** Location metadata could enable technical enforcement of rules like data residency or emissions tracking, reducing reliance on costly manual audits.
- **High-rigor “Level 5 proofs.”** For contexts like international agreements, arms control, or high-stakes emissions auditing. These remain speculative but help define what the upper bound of robustness might look like.

---

## **Closing**

Location proofs sit at the intersection of technology, policy, and economics. My stance is cautious optimism. We’re not chasing mathematical certainty; we’re building open, durable, opt-in systems that raise the cost of lying about where things happen.

There’s much more to figure out. I’d like this to be a conversation, not a declaration. If you’re researching, building, or simply thinking about these questions, I’d love to hear from you.