---
date: 2026-03-18T21:30:00-00:00
description: "Scan, review, curate and fix metadata of Rust crates"
title: "T-Rust - In Rust we Trust"
---

<!--
SPDX-FileCopyrightText: 2026 Contributors to the T-Rust project

This program and the accompanying materials are made available under
the terms of the Apache License Version 2.0 which is available at
https://www.apache.org/licenses/LICENSE-2.0

SPDX-FileType: TEXT
SPDX-License-Identifier: Apache-2.0
-->

## Scan, review, curate and fix metadata of Rust crates

[crates.io](https://crates.io/) hosts over 160.000 Rust packages that have been downloaded over 90 billion times. The origin metadata and licensing documentation for Rust crates is declared by the authors as part of the metadata, but can be misleading or incorrect. Accurate origin and license metadata for Rust crates is essential to safely automate the consumption of Rust packages in the software supply chain of safety- and mission-critical applications.

T-Rust intends to fix this problem in multiple steps: it will scan, review, curate and fix the metadata of the most popular crates. This data will be released as open data, working with the Rust community to provide the data as part of the crates.io API, cross-check and report code borrowing and reuse between crates. Subsequently an AboutCode toolchain will be deployed as a service for all crates authors to review, validate and enrich metadata. The outcome should be be that `crates.io` packages come with better, more accurate origin and license metadata at creation time. The increased level of trust in Rust crates will make it easier to consume more Rust packages safely.

## Run by [AboutCode](https://aboutcode.org)

This project is funded through the NGI0 Commons Fund, a fund established by [NLnet](https://nlnet.nl/) with financial support from the European Commission's [Next Generation Internet programme](https://digital-strategy.ec.europa.eu/en/policies/next-generation-internet-initiative), under the aegis of DG Communications Networks, Content and Technology under grant agreement No 101135429. Additional funding is made available by the Swiss State Secretariat for Education, Research and Innovation ([SERI](https://www.sbfi.admin.ch/)).

&nbsp;

![Abstract logo of four people seen from above](/img/nlnet.webp "NLnet Foundation")
&nbsp;
![Logo of the European Commission](/img/logo-ec.svg "European Commission")

&nbsp;
