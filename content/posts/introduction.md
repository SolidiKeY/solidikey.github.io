---
title: "SolidiKeY Project Kicked Off!"
date: 2023-09-24T19:36:00+02:00
draft: false
---

We are thrilled to announce the kick-off of the **SolidiKeY** project, which is generously supported by the [*Ethereum Foundation*](https://ethereum.org/en/foundation/) and the [*Swedish Research Council*](https://www.vr.se/english.html).

The project name, "SolidiKeY", combines "[Solidity](https://soliditylang.org/)", the most widely used programming language for developing *smart contracts* for the Ethereum blockchain, and "[KeY](https://www.key-project.org/)", a long term endeavor, and tool, for deductive verification of object-oriented programs, in particular Java.

The goal of **SolidiKeY** is to offer to the community a methodology and tool for specifying and verifying Solidity smart contracts. For that, we are developing a totally new version of the KeY system, fully tailored to Solidity.

## What is KeY?

The main incarnation of KeY is a deductive verification tool for Java, and without doubt the main player in that domain. See also the [KeY book](https://www.key-project.org/thebook2/). Among the major case studies of KeY is the discovery and fixing of a bug in the main sorting routine (`Collections.sort()`) of all major Java platforms (incl. OpenJDK and Android). The KeY team has long term experience with source code verification of object-oriented programs, and has developed logics, calculi, and proof systems which are designed specifically for verifying object-oriented languages. This makes smart contracts a natural target for the KeY methodology, because smart contracts naturally relate to the object-orientation.

## What will SolidiKeY be?

While the aforementioned similarities between object-oriented languages and smart contracts provide a good starting point for the R&D in this project, we do *not* aim at translating smart contracts into any other language which KeY already supports.
In KeY style tools, the programming language (here Solidity), is not translated away. Instead, a dedicated proof calculus is developed especially for the language at hand. The calculus interleaves (forward) symbolic execution, logical reasoning about programs, quantifier elimination, and the executable axiomatization of the specific data types at hand. The reasoning machinery does not rely on back-end SMT solvers, and instead handles also the solving part by internal proof rule application, interleaved with other proof steps, with the help of configurable strategies. Through these principles, the logic and proofs "talk" directly about artifacts familiar to the programmer. KeY style provers are largely automated, but allow for interactive steps if the prover cannot discard a problem all alone, thereby pushing the boundaries of what can be verified (without resorting to all too general frameworks, like higher-order logic, which is much harder to use by programmers).

## Why does it matter?

Ethereum smart contracts offer great opportunities for many applications, allowing to
move agreed schemes of asset/commitment exchange to a blockchain ecosystem
that guarantees uncompromised execution of the agreement, without relying on a
third party. However, the strong guarantees provided by the Ethereum blockchain
infrastructure do not themselves prevent problems caused by the programming of the
application layer, i.e., the smart contracts themselves. It is difficult for the smart
contract programmer to foresee all effects of arbitrary behavior of the contract’s
environment. In cases where unforeseen environmental actions can lead to unintended
behavior of the contract, this can result in severe damage to well-behaved users. Smart
contracts are openly available and can be analyzed by everyone for weaknesses to be
exploited, which is actually what happens regularly, even on a large scale. The Ethereum
community has therefore a high interest in methods and tools which support smart
contract programmers in developing contracts that are guaranteed to only exhibit the
intended behavior, to be verified before deployment. But even after deployment, the
resulting evidence shall support contract users, in the sense that they know with
certainty which effects the usage of some contract will have on them. The need for such
methods and tools is widely acknowledged by the community and has been addressed
by several projects and tools aiming to verify Ethereum smart contracts.

## What will you be able to do with SolidiKeY?

With SolidiKeY, you will be able to verify that the flow of assets (Ether as well as tokens) from and to a smart contract can only happen in intended ways. This is done by showing that, under all circumstances, the internal data of the contract is in sync with the external asset flow from and to the contract's users.
This viewpoint brings the requirements that can be verified closer to the user's perspective on the contract, such that users can rely on the specification of the service a contract provides to them. As an example, imagine an auction contract where users can place initial bids, increase bids, and withdraw bids until the auction is closed. One possible user-level requirement could be the following: Once the auction is closed, every user who did not win the auction will get back the sum of all funds (s)he has invested into the contract, minus everything which has been withdrawn. To verify such a requirement, a system needs to reason about both, the internal data, the external flow of assets, and the relation between the two. Supporting the specification and verification of such asset flow-related requirements, in a user-friendly and efficient manner, is what the SolidiKeY project sets out to deliver.

## People

The SolidiKeY project will be driven by the following people:

- [Wolfgang Ahrendt](https://www.cse.chalmers.se/~ahrendt/), Chalmers University of Technology, Gothenburg, Sweden
- [Guilherme Horta Alvares Da Silva](https://www.chalmers.se/en/persons/alvares/), Chalmers University of Technology, Gothenburg, Sweden
- [Richard Bubel](https://www.informatik.tu-darmstadt.de/se/gruppenmitglieder/groupmembers_detailseite_51008.en.jsp), Technical University Darmstadt, Darmstadt, Germany

