---
layout: post
title: "Marketplace EU VAT library notes"
date: 2024-07-04 12:00:45 +0200
tags: vat oss notes
---

Recently, we started our summer product sprint session. Our first idea was to create an **MVP** (Minimum Viable Product) for an open-source marketplace engine.

But after 2 days, we stumbled across the VAT problem. We are located in Switzerland and our target market is CH & EU, we concluded that this was a real pain point, and that our marketplace engine not tackling this issue would result in us reinventing the wheel, with less firepower than competiton.

After some research, we finally found [this document](https://vat-one-stop-shop.ec.europa.eu/guides_en) that allowed us to start to understand the EU VAT reform supposed to happen in 2025.

## Research results

- How is it that it is so hard to find information on something that is mandatory for you to implement to run your business legally in CH & EU?
- Some good **OSS** (Open Source Software) exists e.g. [node-sales-tax](https://github.com/valeriansaliou/node-sales-tax) for simple use cases but they do not fit the marketplace issue.
- There are some commercial actors providing API integrations to tackle this problem, but these solutions are often expansive and opaque.
- There are some famous payment providers tackling the issue, obviously in exchange of a growing share of your transactions.

## Idea: Tackle the e-commerce VAT issue with OSS.

We want to create a open source framework that allows users to implement VAT compliance within their e-commerce / marketplaces projects.

### Why we want to do this

- **Public interest:** We think the e-commerce VAT reform is good from a philosophical perspective it's aim is to maintain fair competition on the market, nonetheless as other regulations eventhough it's aimed at big players the one to suffer will be SMEs as they don't have the means to remain compliant.
- **Private interest**: It is a bottleneck for some of our projects. It can bring us credibility, which can bring us business, in the end we are still a for-profit org. We like to solve puzzles.

### MVP high-level specification

- MVP Scope would be: EU + CH.
- It should have a [Permissive software license](https://en.wikipedia.org/wiki/Permissive_software_license) so that it can be integrated into commercial software.
- Use [EU Commission note](https://vat-one-stop-shop.ec.europa.eu/guides_en) as Guideline document, the goal is not provide Tax Advice but rather to provide / test an implementation that would prove to be reasonnably compliant with EU guidelines.
- It has to be usable as a library as is, we liked `node-sales-tax` JSON minimal database approach, nonetheless it would not be viable on the long run as production users would need a way to connect to a centralised & maintained database.
- It should be transactional, meaning that the library should be able to give VAT rates details for a single transaction.
- It should tackle the Deemed Supplier problem (who is responsible for VAT collection in the marketplace case).
- It should handle transactions for 3+ parties, a transaction between more than 2 parties being a composition of 2 parties transactions.
- It should be able to return an "archive" object on request for a transaction, which would contain legally required information that e-commerce platforms must archive for 10 years.
- We need to create a User Interface to allow non-tech people to test our library.
