---
title: Specification Analysis
weight: 1
---
# Specification Analysis
In this work, we explore the use of LLMs to interpret context-dependent rules and nested structural constraints in PKI systems and X.509 certificates. We acknowledge that these efforts are still at an early stage and are working to further refine them. We welcome feedback and suggestions from the community and provide a brief overview of our current approach below.


## Specification Scope
The CA/Browser community enforces constraints primarily through the Baseline Requirements (BRs), and some CAs additionally check compliance with RFC 5280 before issuing certificates. However, certain domain-specific constraints not explicitly covered by RFC 5280 or the BRs also play an important role in PKI security. To address this, we considered all documents relevant to Unicert issuance, parsing, and validation. Ultimately, our analysis shows that RFC 5280 and the BRs are the most decisive, but our scope also included the PKIX specifications (RFC 3280, 5280), their updates (RFC 9549, 9598, 6818), reference documents (RFC 3490, 1034, 3454), related standards (RFC 6125, the IDNA suite), and the CA/B Forum Policy.

![rfc-dependency](https://zeriny.github.io/unicert/figs/rfc-dependency.png)

## Analysis Steps


{{% steps %}}
1. **Extracting relevant standards and incorporating references to reflect their evolution and interdependencies.**
   We filtered field-related sections from the desired documents using a set of specified keywords. We then refined the filtered sections by incorporating references from other specifications (e.g., domain name formats in RFC 1034) and replacing the outdated sections with updates from newer RFCs.

2. **Improving LLM comprehension of background knowledge.**
   Inspired by a prior ``background-augmentation`` method, we incorporated the refined sections as background knowledge to enhance RFCGPT's understanding of Unicert. Since CA/B BRs are not in RFCGPT’s pretraining data, we added their certificate profile content as supplemental knowledge. All knowledge was extracted as line-based text and placed in the ``background context`` fields of the prompt templates. For example, rules listed in tables were reformatted into comma-separated lines.

3. **Prompting the LLM to generate certificate field requirements.**
   We used few-shot learning to prompt the LLM to extract two types of requirements for each certificate field:
(1) valid encoding types and data structures, and 
(2) constraints on encoding and formatting. 
We excluded semantic constraints like field presence, absence, or criticality.
Prompts included input–output examples to guide the LLM in generating requirements in a structured format (e.g., JSON), and directed it to reply ``No`` when standards lacked relevant details, avoiding fabrication.


![prompt-1](https://zeriny.github.io/unicert/figs/prompt1-datastructure.pdf)
![prompt-2](https://zeriny.github.io/unicert/figs/prompt2-requirements.pdf)


{{% /steps %}}