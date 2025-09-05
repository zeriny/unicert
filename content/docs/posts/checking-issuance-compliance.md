---
date: 2025-09-03
linktitle: Checking Issuance Compliance
menu:
  main:
    parent: tutorials

title: Checking Issuance Compliance
weight: 2
---
[{{< badge title="UniCheck" value="Source Code" >}}](https://github.com/zeriny/unicert_checker)


## UniCheck: A Zlint-based Certificate Compliance Checker

### Overview
This repository contains UniCheck, a tool developed to investigate whether Unicode Certificates (Unicerts) comply with current standards.

UniCheck is a customized version of the `zlint` framework, tailored specifically for our research purposes. It extends `zlint`'s functionality to provide in-depth compliance checks for Unicerts, focusing on aspects not explicitly covered by existing lints.

Since this tool was designed for a specific academic study, it directly modifies the `zlint` source code within the `vendor` directory.


### Implementation Details


#### 1. New Lints for Unicert Compliance

We introduced a new directory at `vendor/github.com/zmap/zlint/v3/lints/unicheck/` to house our custom lints. We also relocated existing lints relevant to checking encoding, format, attribute structure, and value normalization to this dedicated directory for better organization and a streamlined focus.


#### 2. Integration with the Lint Registry

To ensure our custom lints are recognized and executed by the `zlint` framework, we modified the project's configuration to include our new directory in the lint registry. This involved adjusting the `config/config.go` and `vendor/github.com/zmap/zlint/v3/zlint.go` files.


The relevant changes ensure that all lints from our `unicheck` directory are included during the initialization of the `zlint` registry.

```golang
    var sourceList lint.SourceList
    if err := sourceList.FromString(o.Config.ZlintIncludeSources); err != nil {
        log.Fatalf("invalid includeSources: %v\n", err)
    }
    registry, err := lint.GlobalRegistry().Filter(lint.FilterOptions{
        IncludeSources: sourceList,	})
    if err != nil {
        log.Fatalf("lint registry filter failed to apply: %v\n", err)
    }
    o.GlobalZlintRegistry = registry

    log.Println("[+] Included source names:", registry.Sources())
    log.Println("[+] Included lints:", len(registry.Names()))
```

#### 3. Usage as a Library
Our application uses the modified `zlint` framework as a library to perform compliance checks on a single X.509 certificate object. The process involves three main steps:

1) Decoding: The certificate's PEM string is decoded into a DER block. Error handling is in place to catch any PEM parsing failures.

2) Parsing: The DER bytes are parsed to create an `x509` certificate object. This step also includes error checks to handle invalid certificate structures.

3) Lint Execution: The `zlint.LintCertificateEx` function is called on the parsed x509 object, using our customized `GlobalZlintRegistry`, to execute all relevant lints. The results are then captured and returned in a structured format.



```golang
    // First, decode PEM string
    certDerBlock, _ := pem.Decode([]byte(pemStr))
    if certDerBlock == nil {
        res := MyZlintRes{
            Sha1:      certSha1,
            Success:   false,
            ErrorInfo: "Failed to parse PEM block containing the certificate",
        }
        resStr, _ := json.Marshal(res)
        log.Println("Failed to parse PEM block containing the certificate")
        return string(resStr) + "\n"
    }

    // Second, parse DER cert bytes and initialized an x509 object
    parsed, err := x509.ParseCertificate(certDerBlock.Bytes)
    if err != nil {
        log.Println("Unable to parse certificate:", err)
        res := MyZlintRes{
            Sha1:      certSha1,
            Success:   false,
            ErrorInfo: fmt.Sprintf("Unable to parse certificate: %s\n", err),
        }
        resStr, _ := json.Marshal(res)
        return string(resStr) + "\n"
    }

    // Third, excecute zlint for one x509 object
    zlintResultSet := zlint.LintCertificateEx(parsed, c.GlobalZlintRegistry)
    res := MyZlintRes{
        Sha1:     certSha1,
        Success:  true,
        ZlintRes: zlintResultSet,
    }

    resStr, _ := json.Marshal(res)
    ...
```