# Desmos

__a social networking ecosystem of the users, by the users, for the users__

Kwun Yeung (kwun@forbole.com)\
Terence Lam (terence@forbole.com)

NOTE: This document is a work-in-progress and we are still actively developing it. All of the contents are subject to change. Your feedback is highly appreciated. Please check our update regularly.

## Table of Contents

- [Desmos](#desmos)
  - [Table of Contents](#table-of-contents)
  - [Summary](#summary)
  - [Problem Statement](#problem-statement)
  - [Solutions - An Overview](#solutions---an-overview)
  - [Desmos](#desmos-1)
    - [Desmos as a chain](#desmos-as-a-chain)
      - [Inflation](#inflation)
      - [Gini-sensitive sublinear voting power](#gini-sensitive-sublinear-voting-power)
        - [Scenario 1: Cosmos Hub as of 30 Jul 2019](#scenario-1-cosmos-hub-as-of-30-jul-2019)
        - [Scenario 2](#scenario-2)
        - [Scenario 3](#scenario-3)
      - [Minimum commission rate](#minimum-commission-rate)
    - [Desmos as a token](#desmos-as-a-token)
    - [Modules](#modules)
      - [Magpie](#magpie)
        - [Magpie Messages](#magpie-messages)
      - [Profile](#profile)
        - [Profile Messages](#profile-messages)
      - [Reputation](#reputation)
      - [Post](#post)
        - [Post messages](#post-messages)
      - [NFT](#nft)
    - [Web Assembly (WASM)](#web-assembly-wasm)
  - [Phanero](#phanero)
    - [Decentralized Microblogging](#decentralized-microblogging)
    - [Phanero as fee token](#phanero-as-fee-token)
    - [Minting of Phanero](#minting-of-phanero)
  - [Initial distribution of Desmos](#initial-distribution-of-desmos)
    - [Initial supply](#initial-supply)
      - [A foundation: 15%](#a-foundation-15)
      - [Forbole: 12.5%](#forbole-125)
      - [Early supporters: 2.5%](#early-supporters-25)
      - [Community Pool: 10%](#community-pool-10)
      - [Fundraisers: 60%](#fundraisers-60)
    - [Fundraisers](#fundraisers)
      - [First round (20%):](#first-round-20)
      - [Second round (20%):](#second-round-20)
      - [Third round (30%):](#third-round-30)
  - [Validators](#validators)
  - [Development Plan](#development-plan)
    - [Marketing](#marketing)
  - [Organization and projects](#organization-and-projects)
    - [Forbole Limited](#forbole-limited)
    - [Big Dipper](#big-dipper)
  - [Team](#team)
    - [Background](#background)
    - [Careers](#careers)
  - [Roadmap](#roadmap)

## Summary

Centralized social networks are corrupt. They infringe users’ benefits to maximize their own profits. We believe a social network of the users, by the users, for the users will reshape the scene. Our solution is to provide the backbone for social networks to improve their business model in order to develop a stronger goal congruence between the social networks and their users.

Desmos [ˈdɛsmɒs] is a public blockchain for social media applications. It is similar to Cosmos Hub with different staking and minting modules. It also introduces new modules which are specifically designed for reputation-centric decentralized social networking. One of these modules is Magpie, which provides identity and accountability to validators, delegators and other types of stakeholders with a novel and generalizable temporary key pair using browser-based WASM.

Desmos is also a testbed of different interesting parameters and governance methods. Desmos is suitable for performing this role as we expect it will process quite some meaningful transactions early on. Furthermore, as part of the internet of blockchains, Desmos will act as a regional Hub in South China and Southeast Asia. 

We will acquire early engaging users of Desmos by building a decentralized microblogging platform on top of Big Dipper which is a popular block explorer for Cosmos ecosystem. This platform allows various types of tokens holders within the internet of blockchains to communicate in a decentralized, secured and verifiable manner.

Validators are important to the blockchain space. We hope to make the early stage Desmos a “validators first” project. Engaging validators are crucial to the success of Desmos, as they are not only the security providers but also community builders. We will design our incentivized program and fundraiser to reflect this “validators first” philosophy.

## Problem Statement

Social networks have created more problems than before. These include the surging number of scams and spams, fakes news, the security loopholes, the privacy breaches and the oligopolistic behaviours of a handful of social network behemoths that infringe users’ interests and harm the industry as a whole.

Simply put, these centralized social networks are corrupt. 

Desmos has an initiative to build an ecosystem of decentralized social networks. We advocate for a new business model and a new mindset of social networking.

## Solutions - An Overview

The root of the corruption of centralized social networks is their business model. They are destined to infringe users’ privacy as this is their source of income. There is an inborn conflict of interests between social networks and their users. 

We believe a social network of the users, by the users, for the users will reshape the scene. Our solution is to provide the backbone for social networks to improve their business model. By changing the dynamics between various users and stakeholders of the social networks, we can develop a stronger goal congruence between the social networks and their users.

We define the value of a particular social network as the aggregation of the users’ engagements that have happened on that network. With the help of tokenization, users can obtain their stakes in the network by making engagements. Tokenomics will enable a meta-moderation system based on incentive and penalty to improve the quality of users’ engagements.

We achieve the above goal through Desmos, which is a public blockchain specifically designed for social media applications. The first application of Desmos will be supporting a decentralized microblogging platform.

## Desmos

The name Desmos was inspired from Ancient Greek desmós (δεσμός) which means “bond, relationship”. We use Desmos for both the names of the blockchain and its native staking token.

### Desmos as a chain

Desmos the chain is specifically designed for social media applications. It is built with Cosmos SDK and use Tendermint as consensus engine. While it is very similar to Cosmos Hub, we would like to use it as a testbed of some interesting and experimental settings that may be too costly to be performed on Cosmos Hub. Initially, we would like to test a new inflation rate, a new calculation of share of voting power and implement minimum commission rate.

#### Inflation

We will use the same calculation method for inflation as that of Cosmos Hub. The difference is that we will halve the range of “7% to 20%” to “3.5% to 10%”. We expect Desmos will process meaningful transactions in terms of tokenized social network engagements early on and hence this new inflation rate is sufficient to incentivize staking while avoiding too much dilution on the intrinsic value of Desmos token.

#### Gini-sensitive sublinear voting power

Decentralization is a controversial topic on every blockchain. Once the share of voting power is not sufficiently decentralized, it may create problems like the rich get richer which may then discourage the participation of validators with less financial resources.

We introduce a modified method to calculate the share of voting power to encourage Desmos hodlers (which include validators with skin in the game) to distribute their delegations across a number of validators. Under the new scheme, the effective share of voting power of a validator, VP<sub>(eff)</sub>, will be calculated as follows:

##### VP<sub>(eff)</sub> = (1 - G^3) * VP<sub>(linear)</sub> + G^3 * VP<sub>(log)</sub> , where:

   1. VP<sub>(linear)</sub> is the share of voting power when it is calculated using normal voting power<br>
   2. VP<sub>(log)</sub> is the share of voting power when it is calculated using the logarithm of voting power<br>
   3. G is the Gini coefficient calculated based on the linear voting power across the active validators<br>

Below is the scenario analysis for VP<sub>(eff)</sub> under various Gini coefficients.

##### Scenario 1: Cosmos Hub as of 30 Jul 2019

Gini coefficient = 0.68

[![Case 1 Cosmos Hub](Gini-adjusted%20VP%20%20Case%201%20-%20Cosmos%20Hub.png)](https://github.com/desmos-labs/introduction/blob/master/Gini-adjusted%20VP%20Case%201%20-%20Cosmos%20Hub.tsv)

##### Scenario 2

Gini coefficient = 0.248 (similar to Denmark in 2011)

[![Case 2](Gini-adjusted%20VP%20Case%202.png)](https://github.com/desmos-labs/introduction/blob/master/Gini-adjusted%20VP%20Case%202.tsv)

##### Scenario 3

Gini coefficient = 0.47 (similar to the United States in 2014)

[![Case 3](Gini-adjusted%20VP%20Case%203.png)](https://github.com/desmos-labs/introduction/blob/master/Gini-adjusted%20VP%20Case%203.tsv)

One of the possible downside of sublinear voting power is that it may encourage big Desmos holders to spread its own stake across multiple nodes. We try to mitigate this risk by:

- Target our early-stage fundraising to validators with proven track record
- Impose a more stringent cap to the investment allowed per participation
- Allocate more distribution to a series of incentivised campaigns

While this risk cannot be eliminated, we think this is a good experiment for the Cosmos ecosystem at large.

#### Minimum commission rate

(We are considering some mechanisms to avoid price war. We are interested in applying this [suggestion](https://forum.cosmos.network/t/proposal-are-validators-charging-0-commission-harmful-to-the-success-of-the-cosmos-hub/2505/33?u=bharvest) by Hyung of B-Harvest)

### Desmos as a token

Desmos the token is the native staking token on Desmos chain which serves as a license for its holders to contribute to the security and governance in exchange for the incentives.

### Modules

#### Magpie

To provide identity and accountibilty of validators in different chains on Desmos, we need a bridging mechansim to link between the identity from the working chain, e.g. Cosmos Hub, to a temporary identity on Desmos which can operate corresponding social interactions. [`Magpie` (bridge)](https://en.wikipedia.org/wiki/Qixi_Festival) is serving this purpose.

`Magpie` works like the [`SESSION`](https://en.wikipedia.org/wiki/Session_(computer_science)) of a web application. When a user would like to start a conversation, a temporary Desmos key will be created on the client application. The client application will then sign an empty session message using the key of the working chain and embed the signature to a session creation transaction on Desmos signing with the just created temporary Desmos key.

When Desmos receives the session creation transaction, it will not only validate to see if the transaction can be processed. It will also validate the embedded working chain signature with the public key provided. If the signature can be validated, it verifies the identity of the working chain and allows the user with this identity to operate any social interactions on Desmos using the temporary key created and stored on the client application.

_(insert an illustration explaining the mechansim)_

`Magpie` will store a `Session` object in the following structure.

``` go
type Session struct {
    ID            string
    Owner         sdk.AccAddress
    Created       time.Time
    Expiry        time.Time
    Namespace     string
    ExternalOwner string
    Pubkey        string
    Signature     string
}
```

Each `Session` has an expiry time. Once the expiry time is reached, the temporary key (`Session.Owner`) can not be used and a new `Session` has to be created with a new temporary key to work with.

The `Session` expiry time can be extended if the temporary key keeps having activities within a `SessionPeriod`.

##### Magpie Messages

MsgCreateSession \
MsgCloseSession

#### Profile

The `Profile` module let users maintain their public user profile. It is also the public profile of a validator. A `Profile` object is attached to each working chain so that a validator / delegator can have their own profile for each chain.

``` go
type Profile struct {
    ID                  string
    Namespace           string
    ExternalOwner       string
    Moniker             string
    Bio                 string
    Location            string
    Website             string
    KeybaseSuffix       string
    Reputation          int64
    Created             time.Time
    Modified            time.Time
    ReputationModified  time.Time
}
```

A `Profile` can be created and updated after an active `Session` is established.

##### Profile Messages

MsgCreateProfile \
MsgUpdateProfile

#### Reputation

The `Reputation` module calculates the reputation of a user based on the activities she has done. This feature will be used by other modules to update users' reputations for every chain they have registered on Desmos.

#### Post

The `Post` module is used for posting messages on Desomos. Users can also make comment, upvote and downvote to a message. These interactions will trigger the `Reputation` module to caluculate the latest `Reputation` of a user and `Minting` module to mint the new `Phanero`.

A `Post` object is in ths following structure.

``` go
type Post struct {
    ID            string
    ParentID      string
    Message       string
    Created       time.Time
    Modified      time.Time
    Votes         uint
    Owner         sdk.AccAddress
    Namespace     string     // External service namespace, e.g. cosmos
    ExternalOwner string     // External owner address of the post
}
```

##### Post messages

MsgCreatePost \
MsgEditPost \
MsgUpVote \
MsgDownVote

#### NFT

Distribute badges to users based on reputation, tasks completed, etc.

We will be using the [Cosmos NFT module](https://github.com/cosmos/cosmos-sdk/tree/billy/nft/x/nft).

### Web Assembly (WASM)

Send Desmos transactions from the client side. It includes a key manager and functions of broadcasting tranasctions.

## Phanero

### Decentralized Microblogging

Adoption of technology usually starts with a handful of visionaries. We will acquire the early users of Desmos by building a microblogging platform on top of Big Dipper to solve one pain point: the existing and new validators and delegators do not have a way to communicate with each other through a verifiable manner. As Big Dipper is one of the most popular block explorers for Cosmos ecosystem, many people who are interested in Cosmos will definitely visit Big Dipper. A decentralized microblogging platform secured by validators is an interesting way for these users to connect. 

### Phanero as fee token

Phanero [fəˈnærəʊ] is the fee token on the microblogging platform. The name is inspired from Ancient Greek phanerós (φανερός) which means “visible, manifest, evident”. We first knew about this word from Jae Kwon, the cofounder of Cosmos, in his speech in CryptoEconomics Security Conference 2017 (click [here](https://youtu.be/8Eex-wQ5yYU?t=23) for the speech):

> “… I feel like, between crypto and economics there’s another word that’s missing which stands for the transparency, so maybe crypto economics should be crypto phanerós economics …”

> “… there’s this duality between hiding something and sharing something, and what blockchain does or what bitcoin has done it’s shown us a way to coordinate ourselves in a new way by using cryptography to share information and not share information in ways that were not possible before and thereby creating a new ecosystem.”

The literal meaning of phanerós is exactly what we want to achieve in Desmos.  

### Minting of Phanero

The value of a social network is reflected by the sum of all quality users engagements on the network. So the design philosophy of the tokenomics of Phanero is to encourage quality users engagements. The minting of Phanero will directly relate to the creation of users' engagement on our microblogging platform. Initially, we suggest below minting method:

| Engagements  | Change of Phanero |
| --- | ---:|
| Register an user account | `+ 100` |
| Post a message | `-  10` |
| Post a comment on an external message | `+   5` |
| Receive an external  comment | `+   5`  |
| Receive an external share | `+   3`  |
| Receive an external upvote | `+   2`  |
| Receive an external downvote | `+   1`  |

The minting method of Phanero can be changed by on-chain governance of Desmos.

## Initial distribution of Desmos

On most of the PoS blockchains, the distribution of tokens has a tremendous impact on the degree of decentralization. We hope to provide a fairer chance for different people to participate through different types of efforts while ensure the security level of the chain.

### Initial supply 

The initial supply will be around 100,000,000 Desmos. This will be distributed in stages in approximately 12 months after we officially announce the project. The target time for this announcement is before the end of Sept 2019.

#### A foundation: 15%

[Note: We are considering both non-profit or  profit type of entity which support the ecosystem by making investment to ecosystem project such that the foundation is self-sustainable. This is subject to further legal opinions.]

#### Forbole: 12.5%

- 5.0%: Incentive pool to early employees (including cofounding members)
- 7.5% to Forbole Limited

#### Early supporters: 2.5%

This group means the angel investors of Forbole who have made their investment on or before Oct 2018.

#### Community Pool: 10%

This pool will be distributed to qualified participants in a series of incentivised programs before the launch of mainnet. The timing of these programs will relate to various rounds of fundraisers such that our projects, our community and our stakeholders will grow and evolve together.

#### Fundraisers: 60%

See blow section.

### Fundraisers

60% of the initial supply will be distributed throught three rounds of private fundraisers (through simple agreement for future tokens, “SAFT”) before mainnet launch.

#### First round (20%): 

We target to raise USD1 million at USD5 million valuation cap. This round is strictly invited-only. The target SAFT buyers are the experienced and engaged validators and investors on Cosmos ecosystem chains.

#### Second round (20%): 

[to be announced]

#### Third round (30%): 

[to be announced]

## Validators

We will invite validators with proven track records to join our first testnet. We believe the balance between diversity and quality is very important. As such, we will consider a basket of factors such as technical knowledge, community relationships, languages and locations. 

The limit of validator set at genesis will depend on the performance of the testnets.

## Development Plan

### Marketing

## Organization and projects

### Forbole Limited

Forbole Limited (“Forbole”) is a for-profit company limited incorporated in Hong Kong in Oct 2017. The main businesses of Forbole will be staking-as-a-service and technology solution. Forbole is the team to work on Desmos and Big Dipper.

### Big Dipper

Big Dipper, is an award-winning open-source block explorer and delegator tool for Cosmos ecosystem chains used by people from over 130 countries. It is currently exploring [Cosmos Hub](https://cosmos.bigdipper.live/validators?sort=votingPower&dir=-1_), [Iris Hub](https://iris.bigdipper.live/validators?sort=votingPower&dir=-1), [Terra Money](https://terra.bigdipper.live/validators?sort=votingPower&dir=-1), [Kava](https://testnet-1.kava.bigdipper.live/validators?sort=votingPower&dir=-1), [BitSongs](https://testnet-1.bitsong.bigdipper.live/validators?sort=votingPower&dir=-1), [Sentinel](https://explorer.sentinel.co/validators?sort=votingPower&dir=-1), [Cyber Congress](https://cyberd.ai/validators), [LikeChain](http://35.226.174.222/) and [Regen Network](http://bigdipper.regen.network). You can check the repo of Big Dipper [here](https://github.com/forbole/big_dipper).

Another related project is a Bot that monitor the chain when something happened to a specific validator, and send alert through Telegram. It sends alert every 15 seconds, if there is something happened during that time. You may check this [repo](https://github.com/forbole/gaia_bot_monitor).

## Team

### Background

In mid of 2017, after nearly 8 years of partnership in running a digital agency, Kwun and Terence would like to apply blockchain technology to change social networks which are monopolized by centralized powers who abuse users’ privacy to maximize their own benefits. They came up with an idea of a decentralized business network to encourage people to help other to succeed by referring suitable business and career opportunities with each other. They then cofounded Forbole Limited in Oct 2017 to pursue this goal.

In late 2017, while searching for the suitable technology to build this decentralized business network, they stopped at Tendermint. They further discovered Cosmos project and were fascinated by its vision. They started to use Cosmos SDK, which was still in its early stage, to build a testnet.

They knew that they needed some validators to run the testnet. So they started to learn how to become a validator by participating in the testnet of Cosmos Hub and the [validators community](https://blog.cosmos.network/q-a-session-three-cosmos-validators-share-their-experience-ce6501a5d61c).

At the same time, they also needed a blockchain explorer for Forbole’s testnet. They were not satisfied with the official explorer and hence they decided to build one. In August 2018, HackAtom 3 was announced. So they improved the UI design of their explorer and gave it a name to participate the competition. This was how [Big Dipper](http://cosmos.bigdipper.live) was born. It earned a prize in [HackAtom 3](https://blog.cosmos.network/hackatom3-winners-announced-95933b6e23b5).

In Feb 2019, Forbole completed the famous [Game of Stakes](https://blog.cosmos.network/game-of-stakes-closing-ceremonies-eddb71d3b114) as a named winner in the Never Jailed category.

Forbole is recognized through its works in Cosmos ecosystem. With this worldwide traction, now is the right time to resume the development of decentralized social network. We start with Desmos, which will be a Cosmos ecosystem chain specific for social media. Its first application will be a microblogging platform to be integrated to Big Dipper. With the working prototype of this concept, we have won a prize in [HackAtom Seoul](https://blog.cosmos.network/cosmos-hackatom-seoul-winners-d6badbd0629b) in Jul 2019.

### Careers

We are expanding our distributed team across the globe. If you share the same vision with us to disrupt the status quo in social network, come to join us! Please refer to this [repo](https://github.com/forbole/careers) for the job openings of Forbole.

## Roadmap

| Time  | Milestones |
| --- | ---|
| Aug - Sept 2019 | Communicate with potential partnering validators and community contributors |
| Before Sept 2019 | Officially announce Desmos project |
| Nov 2019 | launch the first incentivised testnet |
