# Desmos

**social networks of the users, by the users, for the users**

Kwun Yeung (kwun@forbole.com)\
Terence Lam (terence@forbole.com)

**NOTE: This document is a work-in-progress and we are still actively developing it. All of the contents are subject to change. Your feedback is highly appreciated. Please check our update regularly.**

If you are interested to participate this project, feel free to indicate it by submitting this [Desmos Co-Builders Sale form](https://docs.google.com/forms/d/e/1FAIpQLScLTrzVWRBUEIK5yCatpSpPVbl2G5b16_KvynldjATIu9fc4Q/viewform) (non-binding)

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

## Problem Statement

## Solutions - An Overview

## Desmos

### Desmos as a chain

#### Inflation

#### Reward Distribution

#### Validators set

### Desmos as a token

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

### Phanero as fee token

### Minting of Phanero

## Initial distribution of Desmos

### Initial supply 

#### Foundation

#### Community

### Fundraisers

## Validators

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
