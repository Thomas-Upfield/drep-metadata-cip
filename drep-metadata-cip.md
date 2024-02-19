---
CIP: ?
Title: DRep Metadata
Category: ?
Status: Proposed
Authors:
    - Thomas Upfield <thomas.upfield@iohk.io>
Implementors: []
Discussions:
    - https://github.com/cardano-foundation/CIPs/pull/?
Created: 2024-02-07
License: CC-BY-4.0
---

<!-- Existing categories:

- Meta     | For meta-CIPs which typically serves another category or group of categories.
- Wallets  | For standardisation across wallets (hardware, full-node or light).
- Tokens   | About tokens (fungible or non-fungible) and minting policies in general.
- Metadata | For proposals around metadata (on-chain or off-chain).
- Tools    | A broad category for ecosystem tools not falling into any other category.
- Plutus   | Changes or additions to Plutus
- Ledger   | For proposals regarding the Cardano ledger (including Reward Sharing Schemes)
- Catalyst | For proposals affecting Project Catalyst / the Jörmungandr project

-->

## Abstract
The Conway ledger era ushers in on-chain governance for Cardano via [CIP-1694 | A First Step Towards On-Chain Decentralized Governance](https://github.com/cardano-foundation/CIPs/blob/master/CIP-1694/README.md), with the addition of many new on-chain governance artefacts. Some of these artefacts support the linking off-chain metadata, as a way to provide context.

The [CIP-100 | Governance Metadata](https://github.com/cardano-foundation/CIPs/tree/master/CIP-0100) standard provides a base framework for how all off-chain governance metadata should be formed and handled. But this is intentionally limited in scope, so that it can be expanded upon by more specific subsequent CIPs.

This proposal aims to provide a specification for off-chain metadata vocabulary that can be used to give context to CIP-100 for DRep registration, updates and retirement. Without a sufficiently detailed standard for DRep metadata we introduce the possibility to undermine the ability of DReps to explain their motivations and therefore people looking for someone to represent them with the best possible information available to make that choice. Furthermore a lack of such standards risks preventing interoperability between tools, to the detriment of user experiences.


## Motivation: why is this CIP necessary?
Blockchains are poor choices to act as content databases. This is why governance metadata anchors were chosen to provide a way to attach long form metadata content to on-chain events. By only supplying an On-Chain hash of the off-chain we ensure correctness of data whilst minimising the amount of data posted to the chain.

#### For people wishing to delegate their voting power
When observing from the chain level, tooling can only see the content and history of DRep registration, update and retirement certificates and any associated anchors. These on-chain components do not give any context to the motivation of a DRep. Although this information would likely be the desired context for people who might delegate their voting power. By providing rich contextual metadata we enable people choosing a DRep to delegate their voting power to, to make well informed decisions.

#### For all participants
By standardising off-chain metadata formats we facilitate interoperability for tooling which creates and/or renders metadata attached to DRep registration, update and retirement transactions. This in turn promotes a rich user experience between tooling. This is good for all governance participants.

## Specification
CIP-1694 specifies that metadata anchors are optional for DRep registration, updates and retirement transactions. This CIP covers metadata for the aforementioned transaction types, but it does not cover metadata for voting transactions. 

### Markdown Text Styling
Like [CIP-108](https://github.com/Ryun1/CIPs/blob/governance-metadata-actions/CIP-0108/README.md#markdown-text-styling) this standard includes the possibility of using Github markdown text styling within fields.

### Extended Vocabulary
The following properties extend the potential vocabulary of CIP-100's `body` property.

### Witnesses
DRep Metadata will not follow the CIP-100 specification related to signing the metadata, instead they are attached to a DRep registration. 

#### For Registration and Updates 
`picture`
- Optional 
- A base 64 encoded profile picture
- Moderation of this image must be handled on the client side to comply with their TOS

`username`
- Compulsory
- A very short freeform text field. Limited to 80 characters.
- This SHOULD NOT support markdown text styling.
- Authors MUST use this field for their profile name/ username.
- Authors SHOULD attempt to make this field unique whilst also avoiding crass language.

`socials`
- Compulsory
- A list of urls to the social media/ websites associated with the DRep
- Maximum number??
- It is up to the client to check where these links go
- Warning about linking to external links

`bio`
- Compulsory
- A freeform text field.
- This SHOULD support markdown text styling.
- This SHOULD be used by the author to discuss their ideas, qualifications and motivations, are you part of a company or other organisation.
-- I.e. “I have provided x value to the community already as a developer on y project, and this is why I’d be a great DRep for you…”

`donotlist`
- Optional
- If not included then the value is assumed to be false
- A boolean expression
- A true value means that the DRep does not want to show up in tooling that displays DReps. 
-- I.e. they do not want to appear in GovTool’s DRep Explorer feature

#### For Retirement
`reason`
- Optional
- Providing the rationale for why the DRep retired

### Application
DRep metadata must include all compulsory fields to be considered CIP-???? compliant. As this is an extension to CIP-100, all CIP-100 fields can be included within CIP-???? compliant metadata.

### Test Vector
See test-vector.md for examples.

### Versioning
This proposal should not be versioned, to update this standard a new CIP should be proposed. Although through the JSON-LD mechanism further CIPs can add to the common governance metadata vocabulary,

## Rationale: how does this CIP achieve its goals?
We intentionally have kept this proposal brief and uncomplicated. This was to reduce the time to develop and deploy this standard. This way we enable tooling which depends on this standard to start development. The fields which have been chosen for this standard are heavily inspired by those that we are seeking to introduce for GovTool. We did this because GovTool will likely be the first technical implementation of this standard. 

## Open Questions
1. ~~Do we allow profile pictures to be included in metadata~~ <-- YES! possibly a list of pictures.
2. Do we need to replace the `bio` field with a more structured set of fields
3. Can we include and verify an ADA handle to uniquely identify a DRep
4. ~~What do we do about lack of metadata integrity~~ <-- not show the metadata and make it clear that the #metadata =/ metadata#
5. ~~Should we split this CIP up into separate transactions or also add the vote transaction metadata~~ <-- the scope is fine
6. Compulsory vs optional for all fields
7. types of DRep (script? representing an organisation? want delegations?)
8. How can we verify the information that we are displaying(?) 
9. Tooling providers displaying data SHOULD warn people that none of the information is verified and they should DYOR
10. Tooling providers making metadata SHOULD provide some information about best practices such as putting DRep ID in twitter bio.
11. ~~What do we care about when someone is retiring?~~ <-- just the reason why
12. When someone updates do we want a 1 line summary of what has changed?
13. Tooling to inform people of recent changes?


## Path to Active

### Acceptance Criteria
<!-- Describes what are the acceptance criteria whereby a proposal becomes 'Active' -->

### Implementation Plan
<!-- A plan to meet those criteria or `N/A` if an implementation plan is not applicable. -->

<!-- OPTIONAL SECTIONS: see CIP-0001 > Document > Structure table -->

## Copyright

This CIP is licensed under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/legalcode). 

