---
title: "Code"
date: 2020-11-30T19:57:59-06:00
draft: false
---

# Open Source Software
My open source code is all visible on [my Github page](https://github.com/travisbrady/) but I collect a few highlights here along with their goals.
### 1. [ocaml-vw](https://github.com/travisbrady/ocaml-vw)
[OCaml](https://ocaml.org/) bindings to the [Vowpal Wabbit](https://vowpalwabbit.org/) machine learning system which is maybe most popular for its Contextual Bandit support but also includes more "standard" support for online classification and regression, Latent Dirichlet Allocation, matrix factorization and others.
### 2. [word2phrase.py](https://github.com/travisbrady/word2phrase)
Python port of T. Mikolov's word2phrase algorithm originally proposed in his [Distributed Representations of Words and Phrases and their Compositionality](https://proceedings.neurips.cc/paper/2013/file/9aa42b31882ec039965f3c4923ce901b-Paper.pdf) from NeurIPS 2013
### 3. [ccard](https://github.com/travisbrady/ccard)
Fast command line utility for the approximate counting of strings. Uses the Loglog-Beta algorithm for distinct values estimation component and Metrohash for hashing. Helpful if you work with lots of text data at the command line.
### 4. [flajolet](https://github.com/travisbrady/flajolet)
OCaml library providing approximate/sketching data structures for things such as distinct values estimation (hyperloglog), approximate set membership (bloom filters), frequency estimation (count min sketch), top-k queries (aka approximate frequency tables). Named for French Computer Scientist [Philippe Flajolet](https://en.wikipedia.org/wiki/Philippe_Flajolet).
### 5. [ocaml-h3](https://github.com/travisbrady/ocaml-h3)
OCaml bindings to Uber's [H3](https://h3geo.org/) hierarchical spatial indexing system.
