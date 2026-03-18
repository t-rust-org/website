---
date: 2026-03-18T21:30:00-00:00
description: "Scan, review, curate and fix metadata of Rust crates"
title: "In Rust we Trust - Curate the Crates!"
---

<!--
SPDX-FileCopyrightText: 2026 Contributors to the T-Rust project

This program and the accompanying materials are made available under
the terms of the Apache License Version 2.0 which is available at
https://www.apache.org/licenses/LICENSE-2.0

SPDX-FileType: TEXT
SPDX-License-Identifier: Apache-2.0
-->

## Context

Rust is emerging as a key programming language for safety-critical applications because of its unique properties, such as improved memory safety.

[crates.io](https://crates.io/) is the essential Rust software package ecosystem (aka. "crates") through which developers can create, share, and consume useful libraries and packages to assemble Rust applications. Crate tools (e.g. `cargo`) are integral parts of the Rust toolchain; the cargo specification describes the crate package format and the metadata stored in the `Cargo.toml` file; and the central crates.io web site enables the instant publication of Rust crates and to install them using an API and web site to interact and find out more information about available crates.

`crates.io` hosts over 160 thousand packages that have been downloaded over 90 billion times.

*[AboutCode open source project](https://aboutcode.org)*: The About stack is a suite of open source code analysis tools including the industry-leading ScanCode toolkit that is used as the reference throughout the industry for accurate origin and license determination, including to support Microsoft's internal open source due diligence operations, and to streamline the license documentation of the .NET framework source code.

## Problem

Rust crate origin metadata and licensing documentation is declared by crate authors as part of crate metadata, but can be misleading and/or incorrect:

- It may not reflect the correct and actual license of the underlying code files, or
- The licensing might be ambiguous like with "Apache and MIT" which really means a choice of Apache-2.0 or MIT license (a common ambiguity across the Rust ecosystem), or
- The origin of the borrowed code may be missing when code may have been borrowed from other sources and copied into a crate, leading to possible incomplete licensing information for compliance and wrong origin declaration for security.

Accurate Rust crate origin and license metadata is essential to safely automate the consumption of Rust packages in the software supply chain of safety-critical applications.

It is not possible to always trust crate metadata in current state of affairs, and each software team and organization that considers open source license compliance and security compliance as important topics needs to analyze, review, curate and eventually correct these metadata locally, and expect an increasingly large amount of resources to repeat this work over and over.

This is now growing into a more pressing issue as new federal regulations in the US and Europe, such as the Cyber Resilience Act, demand correct disclosure of the origin of all third-party packages, license and known security vulnerabilities relevant to a product.

## Solution: 'In Rust We Trust' - Curate the Crates

The proposed solution to this is to raise the trust in Rust crates, following a multi-stage approach:

1. Scan, review, curate and fix the metadata of the most popular crates. Release this data as open data, and work with the Rust community to provide the data as part of the crates.io API. Also cross-check and report code borrowing and reuse between crates.
2. Deploy an open source toolchain as a service for all crates authors to review, validate and enrich the crates and `Cargo.toml` metadata. The outcome will be that crates.io packages will now have better, more accurate origin and license metadata at creation time.
3. Integrate this toolchain for deployment and hosting at `crates.io`.
4. Update the cargo toolchain to integrate the update data and validation feature.
5. Work with the crates authors to help them adopt improved metadata, and own this in the future.

At a high level the outcome will be:

- Validated license and origin metadata for crates (coverage prioritized by popularity),
- Nudging (supporting) the ecosystem to provide better metadata over time,
- Shared centralized metadata from the package scans available in all cases.

The envisioned benefit would be to significantly help improve the trust in Rust packages origin and license and avoid each Rust adopter having to redo and re-vet the provenance of each Rust package included in safety-critical applications (or any application subject to the CRA requirements).

The open source and open data [AboutCode stack](https://aboutcode.org) provides all the required tools to efficiently implement and deploy such a solution including:

- [ScanCode](https://aboutcode.org/scancode/), the industry standard for license detection,
- Package-URL (aka. [PURL](https://ecma-tc54.github.io/ECMA-427/)), the industry standard for package identification, and
- MatchCode and PurlDB, the tools to detect code similarities and origin efficiently.

## Example: What this might look like

To give an idea what kind of feature this proposal might manifest in, consider this mockup output of the cargo deny tool for an imaginary Rust project using the log, rand and (imaginary) dummy crate:

```bash
$ cargo deny list

Apache-2.0 (3): log@0.4.22, rand@0.8.5 ✅, dummy@0.1.0 ❌
MIT (2): log@0.4.22, rand@0.8.5 ✅
```

Normally, cargo deny list will provide a list of all licenses declared by the transitive closure of all crate dependencies, grouped by declared license(s). What we are adding with this proposal is the idea of green check marks and red warning crosses, which indicate that a crate has been explicitly scanned and vetted to conform with its declared license (✅), or has failed the validation (❌). The information feeding this output is gathered and made available via the tools and infrastructure mentioned above.

While the above example is showing the human-readable output format generated by cargo deny, it is of course desirable for machine-readable output (such as json) to also include this kind of information, in a form which allows processing and alerting in downstream toolchains. Additionally, tools like `cargo deny` might use this information to generate error- or warning-level output in cases where wrongly declared or unvalidated crates are used in a project supply chain.

**PLEASE NOTE**: This is a made-up example to illustrate the proposed functionality; this does not imply anything about the truthfulness of the license declarations made by the crates used in the examples. Also, while `cargo deny` is used for this example, we are not committing to or endorsing any specific tools at this point in time.

---

## High Level approach

1. We need to create, curate, refine the licensing data for one or all the crates
2. The usage of this data in Cargo for `cargo deny` should be built into the crates-Cargo infrastructure

&nbsp;
