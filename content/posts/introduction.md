---
title: "Introduction"
date: 2023-08-14T16:32:40+02:00
draft: false
---

## KeY Summary

[KeY](https://www.key-project.org/) is one of the most well know deductive verification tools for [Java](https://www.keyproject.org/thebook2/).
Among the major case studies of KeY is the discovery
and fixing of a bug in the main sorting routine (Collection.sort()) of all major
Java platforms (incl. OpenJDK and Android).

## SolidiKeY Summary

The project aims to produce a Solidity (source code) verification tool, called “SolidiKeY”,
in the style of the [KeY verification tool family](https://www.key-project.org/). 
Each function in Solidity can have a contract (a pre and post-condition) and SolidiKeY will be used to prove that each function respects its. 

## Why

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
In SolidiKeY, it will be possible to verify properties of the contract's balance
and internal data, about the asset flow from and to the users.
This will bring the requirements that can be verified closer to the user’s perspective on the
contract, such that users can rely on the specification of the service a contract provides
to them. As an example, imagine an auction contract where users can place initial bids,
increase bids, and withdraw bids until the auction is closed. One possible user-level
requirement could be the following: Once the auction is closed, every user who did not
win the auction will get back the sum of all funds (s)he has invested into the contract,
minus everything which has been withdrawn. To verify such a requirement, a system
needs to reason about both, the internal data, the external flow of assets, and the
relation between the two. Supporting the specification and verification of such asset flow-related requirements,
in a user-friendly and efficient manner, is what this project sets out to deliver.
To maximize impact and usability, we will support specification and
verification of (untranslated) Solidity code, thereby staying close to the most widely
used Ethereum smart contract language.

## Why this project?

There are numerous approaches and projects which aim to improve or ensure the safety of
Ethereum smart contracts in general, and Solidity smart contracts in particular.
Many methods and tools do some kind of verification of smart contracts.
Linters like SolCheck and others are lightweight static analysis
tools that check mainly for the occurrence of vulnerability patterns or ‘smells’,
which may indicate bugs. They are however not able to check functional correctness,
i.e., compliance with contract-specific specifications. Oyente, Mayan, Manticore, and
Slither are symbolic execution-based static analysis tools, of which some can
check for user-specified properties. They aim to support bug finding and are in contrast
to the SolidiKeY approach not compositional, less expressive, and bound in the symbolic
execution depth. In contrast, SolidiKeY is compositional, allowing verification
independent of the behavior of external contracts. VerX is an automatic
abstraction/refinement-based verifier for Solidity contracts. They use temporal
specification language and their invariants must hold throughout the function
execution, while our invariants only must be intact whenever control is outside the
contract. For re-entrance safety, they rely on checking effective external callback
freedom for a given bundle. This check requires that all external contracts are known a
priori, which I think is a too strong assumption in the potentially hostile environment
which is characteristic of smart contracts. Finally, the group of projects which come
closest to the methodology of the proposed project is deductive verification tools for
Solidity source code. Most of them are based on solver back-ends (SMT and/or Horn
clauses), to which the front-end verification problems are translated. These tools
support the specification of pre-post conditions and contract invariants. For instance,
solc-verify and VeriSol translate Solidity to the intermediate language Boogie, to then
use the Boogie (SMT-based) deductive verification tool. Also, SMTChecker was originally
based on translation to SMT solvers, but by now makes heavy use of Horn-clauses
which Solidity is translated to. Horn-clause solving is then used for model checking and
the generation of counterexamples, including the generation of attack sequences.
Another tool in this class is VeriSmart, which also generates vulnerable transaction
sequences.
SolidiKeY will be also labeled as a deductive verification tool 
for Solidity source code. In contrast to the tools named
above, it follows design choices that are characteristic of the KeY tool family. In KeY
tools, the programming language (here Solidity), is not translated away. Instead, a
dedicated proof calculus is developed especially for the language at hand. The calculus
interleaves (forward) symbolic execution, logical reasoning about programs, quantifier
elimination, and the executable axiomatization of the specific data types at hand. The
reasoning machinery does not rely on back-end solvers, and instead handles also the
solving part by internal proof rule application, interleaved with other proof steps, with 
the help of configurable strategies. Through these principles, the logic and proofs ‘talk’
directly about artifacts familiar to the programmer. KeY style provers are largely
automated, but allow for interactive steps if the prover cannot discard a problem all
alone, thereby pushing the boundaries of what can be verified (without resorting to all
too general frameworks, like higher-order logic, which is much harder to use by
programmers). A dedicated Solidity verification tool based on these principles will offer
a good complement to existing Solidity verification approaches, with very different
trade-offs. In short, the aforementioned (SMT/Horn) solver-based tools may be stronger
in generating counterexamples and attack sequences. On the other hand, SolidiKeY will
push the boundaries of what can be specified and verified, closer to user-level requirements, 
with a focus on asset flow histories. For instance, SolidiKeY will be able to
specify and verify properties that, for each user, relate the final payback from a
contract with the sum of the user’s investments minus the sum of intermediate paybacks.
For that, the financial net a user has with a contract will be available in the
specification language, in the logic, and supported by the symbolic execution and
reasoning machinery. Finally, being based on the KeY ecosystem, SolidiKeY will in the
aftermath of the proposed project, integrate other functionalities from the KeY context,
like automated test-case generation, combined static and runtime verification, and
symbolic debugging, among others.