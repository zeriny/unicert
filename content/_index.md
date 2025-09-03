---
title: Introduction
bookHeadingAnchor: false
layout: landing
---

<div class="main-body">

# Unicert Project

This is the documentation and open-source space for the Unicert project.
We provide the main analysis scripts and datasets used in our paper, "Analyzing Compliance and Complications of Integrating Internationalized X.509 Certificates."

{{< badge style="success" title="Publication" value="Under review" >}} 
<!-- {{< badge style="default" title="Badge" value="Value" >}} -->


</div>


## Introduction

The PKI system supports global use with X.509 certificates, integrating internationalized content like IDNs and multilingual text, referred to as ``Unicerts``. This integration introduces complexity in Unicert issuance and usage.
Past incidents showed that poor Unicode handling can cause security risks, including spoofing and remote code execution,  yet threats specific to PKI and Unicerts remain underexplored.
This paper presents the first large-scale study of Unicerts, examining both issuance and parsing compliance.
By analyzing 34.8M Unicerts from CT logs and 9 mainstream TLS libraries, we found the PKI ecosystem struggles with adopting Unicode.
On the issuing side, 373 CAs issued 249k (0.72\%) non-compliant Unicerts due to weak validation on character ranges, normalization, and formatting, 65.3\% of which were from publicly trusted CAs.
These issues arise from overly complex standard requirements.
On the parsing side, we found that libraries (e.g., GnuTLS and PyOpenSSL) exhibited issues in decoding and handling special characters, such as incompatible decoding and improper escaping, which could lead to incorrect entity extraction or subfield forgery.
We further empirically identified three threat surfaces: user spoofing, CT monitor misleading, and traffic obfuscation. Finally, we analyzed root causes and proposed recommendations to enhance Unicert compliance in the global PKI ecosystem.

{{<button relref="/docs/introduction">}}Details{{</button>}}
