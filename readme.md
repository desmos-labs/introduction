# Desmos

#### a social networking ecosystem of the users, by the users, for the users

Kwun Yeung (kwun@forbole.com) <br>
Terence Lam (terence@forbole.com) <br>

NOTE: This document is a work-in-progress and we are still actively developing it. It is subject to change. Your feedback is highly appreciated. Please check our update regularly.

## Table of Contents

- [Summary](#summary)
- [Background](#background)
- [Problem Statement](#problem-statement)
- [Desmos](#desmos)
  - [Desmos as a chain](#desmos-as-a-chain)
    - [Inflation](#inflation)
    - [GINI-sensitive sublinear voting power](#gini-sensitive-sublinear-voting-power)
    - [Minimum commission rate](#minimum-commission-rate)
  - [Desmos as a token](#desmos-as-a-token)
- [Phanero](#phanero)
  - [Minting of Phanero](#minting-of-phanero)
- [Initial distribution of Desmos](#initial-distribution-of-desmos)
- [Organization](#organization)
  - [Forbole Limited](#forbole-limited)
  - [Big Dipper](#big-dipper)
  - [Team](#team)
- [Roadmap](#roadmap)

## Summary

Desmos [ˈdɛsmɒs] is a public blockchain for social media applications built with Cosmos SDK and Tendermint. It is similar to Cosmos Hub with different staking and minting modules. The first module of Desmos is Magpie, which provides identity and accountability to validators, delegators and other types of stakeholders with a novel and generalizable temporary key pair using browser-based WASM. Desmos will gradually include more modules specifically designed for decentralized social networking and digital advertising applications. It will also serve as a regional Hub in South China and Southeast Asia and a testbed of different interesting parameters and governance method.

Initially, we will bootstrap early users by building a decentralized microblogging platform on top of Big Dipper to solve one pain point: the existing and new Cosmonauts do not have a way to know each other through a decentralized and verifiable manner. As Big Dipper is one of the most popular block explorers for Cosmos ecosystem chains, many people who are interested in Cosmos will definitely visit Big Dipper. A decentralized microblogging platform secured by validators is an interesting way for Cosmonauts to connect. 

After experiencing various blockchain projects, we hope to make Desmos a “validators first” project. We believe engaging validators are crucial to the success of Desmos, as they are not only our security guards but also our community builders. This is particularly important to a social network-specific chain like Desmos. We will design our incentivized program and fundraiser to reflect this “validators first” philosophy.

## Background

In mid of 2017, after nearly 8 years of partnership in running a digital agency, Kwun and Terence would like to apply blockchain technology to change social networks which are monopolized by centralized powers who abuse users’ privacy to maximize their own benefits. They come up with an idea of a decentralized business network to encourage people to help other to succeed by referring suitable business and career opportunities with each other. They then cofounded Forbole Limited in Oct 2017 to pursue this goal. 

In late 2017, while searching for the suitable technology to build this decentralized business network, they stopped at Tendermint. They further discovered Cosmos project and were fascinated by its vision. They started to use Cosmos SDK, which was still in its early stage, to build a testnet.

They knew that they needed some validators to run the testnet. So they started to learn how to become a validator by participating in the testnet of Cosmos Hub and the [validators community](https://blog.cosmos.network/q-a-session-three-cosmos-validators-share-their-experience-ce6501a5d61c). 

At the same time, they also needed a blockchain explorer for Forbole’s testnet. They were not satisfied with the official explorer and hence they decided to build one. In August 2018, HackAtom 3 was announced. So they improved the UI design of their explorer and gave it a name to participate the competition. This was how [Big Dipper](http://cosmos.bigdipper.live) was born. It earned a prize in [HackAtom 3](https://blog.cosmos.network/hackatom3-winners-announced-95933b6e23b5).

In Feb 2019, Forbole completed the famous [Game of Stakes](https://blog.cosmos.network/game-of-stakes-closing-ceremonies-eddb71d3b114) as a named winner in the Never Jailed category. 

Forbole is recognized through its works in Cosmos ecosystem. With this worldwide traction, now is the right time to resume the development of decentralized social network. We start with Desmos, which will be a Cosmos ecosystem chain specific for social media. Its first application will be a microblogging platform to be integrated to Big Dipper. With the working prototype of this concept, we have won a prize in [HackAtom Seoul](https://blog.cosmos.network/cosmos-hackatom-seoul-winners-d6badbd0629b) in Jul 2019. 

## Problem Statement

Social networks have created more problems than before. These include the unresting scams and spams, the security loopholes, the privacy breaches and the oligopolistic behaviours of a handful of social network behemoths that infringe users’ interests and harm the industry as a whole. 

The root of the above problems is the structural deficiency of the business model of these centralized social networks. We believe a social network of the users, by the users, for the users will be a solution to reshape social network. 

Desmos has an initiative to build an ecosystem of decentralized social networks. We advocate for a new business model and a new mindset of social networking.

## Desmos

The name Desmos was inspired from Ancient Greek desmós (δεσμός) which means “bond, relationship”. We use Desmos for both the names of the blockchain and its staking tokens. 

### Desmos as a chain 

Desmos the chain is specifically designed for social networking apps. It is built with Cosmos SDK and use Tendermint as consensus engine. While it is very similar to Cosmos Hub, we would like to use it as a testbed of some interesting and experimental settings that may be too costly to be performed on Cosmos Hub. Initially, we would like to test a new inflation rate, a new calculation of share of voting power and implement minimum commission rate.

#### Inflation

We will use the same calculation method for inflation as that of Cosmos Hub. The difference is that we will halve the range of “7% to 20%” to “3.5% to 10%”. We expect Desmos will process meaningful transactions in terms of tokenized social network engagements early on and hence this new inflation rate is sufficient to incentivize staking while avoiding too much dilution on the intrinsic value of Desmos token.

#### GINI-sensitive sublinear voting power

Decentralization is a controversial topic on every blockchain. Once the share of voting power is not sufficiently decentralized, it may create problems like the rich get richer which may then discourage the participation of validators with less financial resources. 

We introduce a modified method to calculate the share of voting power to encourage Desmos hodlers (which include validators with skin in the game) to distribute their delegations across a number of validators. Under the new scheme, the effective share of voting power of a validator, VP<sub>(eff)</sub>, will be calculated as follows:

##### VP<sub>(eff)</sub> = (1 - G^4) * VP<sub>(linear)</sub> + G^4 * VP<sub>(log)</sub> , where:

   1. VP<sub>(linear)</sub> is the share of voting power when it is calculated using normal voting power<br>
   2. VP<sub>(log)</sub> is the share of voting power when it is calculated using the logarithm of voting power<br>
   3. G is the GINI coefficient calculated based on the linear voting power across the active validators<br>

Below is the scenario analysis for VP<sub>(eff)</sub> under various GINI coefficients.

##### Scenario 1: Cosmos Hub as of 30 Jul 2019

GINI coefficient = 0.68

![alt text](https://github.com/desmos-labs/introduction/blob/master/Effective%20VP%20-%20Cosmos%20Hub%2020190730.png)

##### Scenario 2

GINI coefficient = 0.47 (similar to the United States in 2014)

![alt text](https://github.com/desmos-labs/introduction/blob/master/Effective%20VP%20-%20Gini%200.47.png)

##### Scenario 3

GINI coefficient = 0.248 (similar to Denmark in 2011)

![alt text](https://github.com/desmos-labs/introduction/blob/master/Effective%20VP%20-%20Gini%200.248.png)

#### Minimum commission rate

(We are considering a mechanism of minimum commission rate.)

### Desmos as a token 

Desmos the token is the native staking token on Desmos chain which serves as a license for its holders to contribute to the security and governance in exchange for the incentives.

## Phanero 

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

On most of the PoS blockchains, the distribution of ownership of stakes has a direct impact on the degree of decentralization. We plan to improve the decentralization of initial distribution of Desmos to provide a fairer chance for different people to participate through financial capital and sweat capital while ensure the security level of chain.

## Organization and projects

### Forbole Limited

Forbole Limited (“Forbole”) is a for-profit company limited incorporated in Hong Kong in Oct 2017. The main businesses of Forbole will be technology solution service and digital asset management. Forbole is the team to initiate Desmos and Big Dipper.

### Big Dipper

Big Dipper, is an award-winning open-source block explorer and delegator tool for Cosmos ecosystem chains used by people from over 130 countries. It is currently exploring [Cosmos Hub](https://cosmos.bigdipper.live/validators?sort=votingPower&dir=-1_), [Iris Hub](https://iris.bigdipper.live/validators?sort=votingPower&dir=-1), [Terra Money](https://terra.bigdipper.live/validators?sort=votingPower&dir=-1), [Kava](https://testnet-1.kava.bigdipper.live/validators?sort=votingPower&dir=-1), [BitSongs](https://testnet-1.bitsong.bigdipper.live/validators?sort=votingPower&dir=-1), [Sentinel](https://explorer.sentinel.co/validators?sort=votingPower&dir=-1), [Cyber Congress](https://cyberd.ai/validators), [LikeChain](http://35.226.174.222/) and [Regen Network](http://bigdipper.regen.network). You can check the repo of Big Dipper [here](https://github.com/forbole/big_dipper).

Another related project is a Bot that monitor the chain when something happened to a specific validator, and send alert through Telegram. It sends alert every 15 seconds, if there is something happened during that time. You may check this [repo](https://github.com/forbole/gaia_bot_monitor).

### Team

We are expanding our distributed team across the globe. If you share the same vision with us to disrupt the status quo in social network, come to join us! Please refer to this [repo](https://github.com/forbole/careers) for the job openings of Forbole.

## Roadmap
