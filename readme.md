# Desmos

__social networks of the users, by the users, for the users__

Kwun Yeung (kwun@forbole.com)\
Terence Lam (terence@forbole.com)

**NOTE: This document is a work-in-progress and we are still actively developing it. All of the contents are subject to change. Your feedback is highly appreciated. Please check our update regularly.**

## Table of Contents

- [Desmos](#desmos)
  - [Table of Contents](#table-of-contents)
  - [Summary](#summary)
  - [Problem Statement](#problem-statement)
  - [Solutions - An Overview](#solutions---an-overview)
  - [Desmos](#desmos-1)
    - [Desmos as a chain](#desmos-as-a-chain)
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
    - [Fundraisers](#fundraisers)
  - [Validators](#validators)
  - [Organization and projects](#organization-and-projects)
    - [Forbole Limited](#forbole-limited)
    - [Big Dipper](#big-dipper)
  - [Team](#team)
    - [Background](#background)
    - [Careers](#careers)
  - [Roadmap](#roadmap)

## Summary

Centralized social networks are corrupt. They infringe users’ benefits to maximize their own profits. Our solution is to provide the backbone for social networks to improve their business model in order to develop a stronger goal congruence between the social networks and their users.

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

Desmos is a blockchain in the Cosmos ecosystem specific for social networking apps. It uses game theory and on-chain governance to decentralize the business model of social network which prioritize the interests of users. Its position is like Cosmos Hub but with different inflation, reward distribution and validator set. We are studying the feasibility of these interesting settings:

#### Inflation

Can we use fixed inflation amount (eg. 8 million Desmos per year) to make the inflation rate to decrease over time? 

#### Reward Distribution

Is that possible that all validators to share the same amount of rewards? Here is an example. Assuming there is 50 validators and there is 22,000 Desmos as reward for each day, then each validators will receive 440 Desmos. 

This will create a built-in force to equalize the commissions to disincentivize price war.

#### Validators set

Due to the fact that each validator will receive the same amount of reward for each block, we may need to use on-chain governance to  approve the revision of validator set when there is new proposal for this.

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

A user's reputation is related to the following aspects.

1. Activity
2. Post attention
3. No. followers
4. No. likes
5. No. comments
6. No. of shares

The reputation should be a time sensitive figure. A user will lose reputation if she is not active in the community for a period of time.

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

The minting method of Phanero will be decided by on-chain governance of Desmos.

## Initial distribution of Desmos

On most blockchains, the initial distribution of tokens has a tremendous impact on the degree of decentralization later on. We hope to provide a fairer chance for different people to participate through different types of efforts while ensure the security level of the chain.

### Initial supply 

**NOTE: This document is a work-in-progress and we are still actively developing it. All of the contents are subject to change. Your feedback is highly appreciated. Please check our update regularly.**

The initial supply will be around 100,000,000 Desmos. This will be distributed in stages in approximately 12 months after we officially announce the project. The target time for this announcement is before the end of Sept 2019.

| Entities  | % of supply |
| --- | ---:|
| A Foundation | `12.5%` |
| Forbole | `10.0%` |
| Employee Incentive | `5.0%` |
| Early supporters | `2.5%`  |
| Community Pool | `10.0%`  |
| Fundraisers | `60.0%`  |

#### Foundation

The Foundation (to be setup) is similar to ICF but with a more specific focus on developing blockchain as a career through education. Our focus is to promote the development of tools and applications for the new internet: the Interchain. 

#### Community

Most of the other projects allocate a tiny amount for community incentives. This may due to a lot of structural or adminsitrative reasons. But according to our experience as a contributor and validator to other blockchain projects, we understand the importance of community incentive. We decided to set a staggering 10% pool for this.

2.5% is for a guaranteed reward to validators in early stage. Our current target is to support during the 12 months testnet period before mainnet and then another 12 months after mainnet. 

7.5% is for a series of incentivized programs about staking, development and community building. We expect more than half of them will be allocated before the mainnet launch.

### Fundraisers

**NOTE: This document is a work-in-progress and we are still actively developing it. All of the contents are subject to change. Your feedback is highly appreciated. Please check our update regularly.**

People increasingly concern with the centralization problem of some blockchains. Some have argued that the seed of centralization has been sown in early fundraiser.

Validators are more than security providers. They develop tools and build the community. They are Co-builders. We hope to make Desmos a “validators first” project. Our goal is to make validators to have a strong sense of ownership: we are co-building Desmos together.

#### Round-0 (10%-20%): 

In this round, we target to raise USD 1 million at USD 5 million valuation cap. This round is strictly invited-only. We call it "Co-buiders" round. We want to invite 1-0-50 reputable validators/delegators to acquire skin in the game in this earliest fundraiser. Each independent individual can purchase up to [1 million Desmos (USD 50,000)].

#### Round-1a (10%-20%): 

This is a round for the participants of Round-0 to invest more after they have gained more confidence in the project. We plan to start this round 3 months after Round-0 at a valuation cap of USD 10 million.

#### Round-1b (0-20%):

Remaining portion of Round-1b (if any) will be opened for other interested parties probably those who have joined the testnet but missed the previous rounds after about 1 month of Round-1a at a valuation cap of USD 15 million.

#### Third round (20%-40%): 

This will be the last round before mainnet launch. Our target mainnet launch will be happened 12 months after the completion of Round-0.

## Validators

We will invite validators with proven track records to join our first testnet. We believe the balance between diversity and quality is very important. As such, we will consider a basket of factors such as technical knowledge, community relationships, languages and locations. 

The limit of validator set at genesis will depend on the performance of the testnets.

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
| Sep 2019 | Start communication with potential validators, developers and community contributors |
| Oct 2019 | Launch the first private testnet |
| Nov 2019 | Launch the first public testnet |
| Nov 2019 | Finalize Round-0 fundriaser details|
| Dec 2019 | Close Round-0 fundraiser |

2020: to be continued... ...
