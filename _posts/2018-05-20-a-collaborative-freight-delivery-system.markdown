---
layout: post
title:  "A Collaborative Freight Delivery System"
date:   2018-05-20 12:16:46 +0100
categories: jekyll update
---
# Abstract

This article proposes a shipping solution for urban areas with high efficiency and low cost (both economically and environmentally), by providing a transparent and collaborative consolidation platform on top of blockchain.

# Introduction

The problem with goods delivery in high population density areas can be summarised as follows:

{% include note.html content="This part requires references." %}
1. large number of small businesses and individuals requiring goods delivered from a large number of suppliers
2. freight vehicles delivering to locations across large geo-area, causing wasted journeys
3. large number of vehicles causing congestion and pollution

Large retail chains benefits from economy of scale, by consolidating large amount of goods for all shops within a geo area and utilising their own consolidation centers and vehicle fleets.

Such benefit is not always available with small retailers and businesses.  

On the other hand, municipal bodies like the City of London are introducing restrictions on the delivery sector, which will make efficient delivery planning not only a cost saving strategy but also a necessity.

What is lacking is a platform that where all parties can participate to make efficient shipping decisions.  To this end we propose a novel platform based on blockchain technology.

# Blockchain

The blockchain provides a distributed public ledger that records all transactions published by participants.

Ethereum is a blockchain with generic computing power by using constructs called smart contracts.  The state transition of smart contracts is governed by the contract definition and is verified by validators (i.e., miners) of the blockchain.

Such a system can be used to create, track and distribute consensus that is irrefutable and unchangeable, without the need for a central authority.

# A Verification Game

The goal of the proposed design of the consolidation platform (refered to as "the platform" from now) is to allow decisions about goods delivery to be made and tracked by all interested parties.

We identified the following players in the platform:

1. Businesses with delivery requirements ("the business")
2. Freight companies and consolidation depots ("the shipper")
3. 3rd parties providing shipping strategies as well as validating the strategies ("the solver")
4. Municipal authority responsible for regulation and administration ("the authority")

Note 3rd parties can include individual as well as other organisations (since the platform is open to the public).  The shippers can also be solvers.

Then a typical working process of the platform would be the following:
1. The authority issues regulations on shipping to locations in a city, in the form of a special contract that is refered to by everyone else.
2. The businesses publish delivery requirements onto the platform
3. The shippers publish their interest in fulfilling the requirements (fulfillments)
4. The solvers group the fulfillments for consolidation and publish the plan to the platform.  Then all businesses and shippers involved in the plan will need to consent to the plan before it becomes a binding contract, after which the shipping process can happen.
5. After the shipping has happened in reality, the businesses or shippers can publish the actual result to the platform, allowing for tracking and auditing by the public.

# Challenges

The above is a high level description of the platform.  There are a number of major challenges that should be addressed before such a system is usable.

## Privacy

Unless a private chain is employed, the data on the blockchain is open to the public, which might pose a privacy issue to businesses and shippers (as competitors can see each others' business data).

Here are some ways the problem can be solved or mitigated:
1. Multi accounts.  One business can create multiple accounts (or even a new account per contract) to prevent people linking their business actions together.
2. Standardised cargo format.  Using standard dimensions (such pallets) and goods types for shipping requirements, without the details of the goods.  
3. Standardised location format.  Location is important for consolidating deliveries, but can also be used to identify the business.  A grid of the city can be used instead (or any division method that makes sense) of precise address, that can still allow consolidation to be calculated.
4. Distributed off-chain storage.  Sensitive data can be stored into systems like [Lightstreams](https://medium.com/lightstreams/smart-contracts-privacy-vs-confidentiality-6fb90c731fde) that has access control (and the public chain only stores hash keys to the data), and the solvers need to be authorised to see the data.  This can be potentially combined with [zero-knowledge proof](https://blockchain.works-hub.com/learn/snarky-a-high-level-language-for-verifiable-computation-25c02) to allow verifiers of the blockchain to decide the correctness of computation without acessing the data.

## Computation Cost

The computation speed of Ethereum is no faster than a mobile phone, and the cost can be significant depending on the demand.

There are plans to make the computation more efficient and cheaper, such as using [proof-of-stake](https://en.wikipedia.org/wiki/Proof-of-stake), [sharding](https://github.com/ethereum/wiki/wiki/Sharding-FAQ) and off-chain computation, but because of the complex nature of consolidation computation, it might be better to split the process into two parts: solving and verifying.

Essentially, the authority will publish a set of rules that define valid consolidation plans (such as time, location and capacity constraints) in the form of a computer program on to the blockchain.

The solvers will create consolidation plans (i.e., **solving** the problem) using whatever program/language they choose, and publish the result onto the blockchain.

The verifiers will use the rules to **verify** that the consolidation plans are valid.  If they're not, then the solvers will be punished (losing their deposits, more on this later).

## Incentives to Do the Right Thing

Obviously we don't want anyone to be able to do anything they want on the platform, so we need to ensure people are incentivised to do the good.

First of all, the roles of each individual on the platform should be verified.  This can be done by using a consensus mechnism so everyone can verify each other's identity.  

Secondly, it is important that misbehaviours (such as giving an invalid consolidation, misreporting a consolidation as invalid) are caught and penalised.  This can be done by using a deposit mechnism similar to proof-of-stake.  

Thirdly, solvers and verifiers need incentives to do their job.  They will be rewarded for consolidations plans that they contribute and the verifications they perform.

There are also other challenges that need to be addressed, such as conflict in consolidation (2 valid consolidations with overlapping parts) and the agreement process, which will be discussed in other papers.

# The Business Model

There are several revenue streams that might be viable:

1. Commission fees.  Each successful consolidation pays out a small fee to the maintainers of the system.
2. Value added services, such as reporting systems powered by data from the platform, professional services helping businesses integrating with the platform, etc.

# Strategy of Adoption

To roll out such a novel system is not easy, and certainly cannot be rushed.

It is imaginable that at the beginning the platform will only act as a slave system that only collects data but is not used for decision making.

Then people can be invited to take part in the platform and evaluate its performance.

# Conclusion

It is possible that the whole system can take several years to adopt, and even more to mature.  But given the urgency of the current situation and the benefits this system provides, it is worth the difficulties.

# References

[https://www.cityoflondon.gov.uk/services/environment-and-planning/planning/design/Documents/City-of-London-delivery-and-service-guidance.pdf](https://www.cityoflondon.gov.uk/services/environment-and-planning/planning/design/Documents/City-of-London-delivery-and-service-guidance.pdf)

[http://www.ftc2050.com/reports/westminster_road_traffic_final_Dec_2016.pdf](http://www.ftc2050.com/reports/westminster_road_traffic_final_Dec_2016.pdf)

[https://s3.amazonaws.com/lightstreams/lightstreams_whitepaper.pdf](https://s3.amazonaws.com/lightstreams/lightstreams_whitepaper.pdf)
[https://medium.com/lightstreams/smart-contracts-privacy-vs-confidentiality-6fb90c731fde](https://medium.com/lightstreams/smart-contracts-privacy-vs-confidentiality-6fb90c731fde)

[https://blockchain.works-hub.com/learn/snarky-a-high-level-language-for-verifiable-computation-25c02](https://blockchain.works-hub.com/learn/snarky-a-high-level-language-for-verifiable-computation-25c02)

[https://eprint.iacr.org/2013/279.pdf](https://eprint.iacr.org/2013/279.pdf)