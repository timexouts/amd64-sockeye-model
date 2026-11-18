
# AMD64 Architecture Model and Formal Verification

AMD64 architecture model developed in [Sockeye](https://sockeye.ethz.ch/) as part of my bachelor's thesis at ETH Zürich.

The project explores formal verification of memory accesses, address translation, privilege isolation, and System Management Mode (SMM).

## Bachelor's Thesis

**Automated Vulnerability Finding by Reasoning About Memory Accesses on a Modern System-on-Chip (AMD64)**

Jan Häussermann — ETH Zürich

[Read the full bachelor's thesis (PDF)](docs/Bachelor.pdf)

## Model Overview

The model covers a subset of the AMD64 architecture, focusing on:

- Processor operating modes and registers
- Memory segmentation and address translation
- Four-level and five-level paging
- Memory protection and privilege checks
- System Management Mode (SMM) and SMRAM

The model is implemented in the Sockeye domain-specific language.

## Verification Results

### Sinkclose Vulnerability

The model successfully reproduced the known Sinkclose vulnerability and generated a counterexample trace demonstrating the attack path.

A separate verification scenario checked a modeled mitigation, which prevented the attack under the model's assumptions.

### User-Mode Isolation

An inductive verification approach was used to check that a user-mode application could not access protected memory regions or modify system resources under the specified assumptions.

The evaluation included base cases for both four-level and five-level paging.

These are verification results for the modeled architecture, not guarantees about every physical AMD64 processor.

## Repository Structure

- `model/amd_ryzen.soc` — Main system model and verification scenarios
- `model/memory.soc` — Memory accesses, segmentation, and paging
- `model/registers.soc` — Processor registers and state
- `model/smm.soc` — System Management Mode
- `model/types.soc` — Shared types
- `model/sinkclose_small.soc` — Smaller Sinkclose proof-of-concept model
- `docs/Bachelor.pdf` — Bachelor's thesis report

## Running the Model

The project requires the [Sockeye framework](https://gitlab.inf.ethz.ch/project-opensockeye/sockeye) and a supported verification backend, such as Rosette.

Example commands:

```bash
sockeye ./model/amd_ryzen.soc -b rosette -s sinkclose_no_device -r
sockeye ./model/amd_ryzen.soc -b rosette -s sinkclose_fix -r
sockeye ./model/amd_ryzen.soc -b rosette -s base_case_PML4 -r
sockeye ./model/amd_ryzen.soc -b rosette -s step_case -r
```

These commands are based on the upstream Sockeye test suite. They have not yet been rerun with this standalone repository.

## Limitations

This is a partial architectural model rather than a full processor implementation.

Features such as caching, TLB behavior, virtualization, and complete exception handling are outside its scope.

Verification depends on assumptions about the architecture, software state, and the correctness of the hardware documentation.

See Chapters 7–9 of the thesis for the implementation details, evaluation, and limitations.

## Sockeye Project

Sockeye is a separate research language and verification framework developed at ETH Zürich. This repository contains the AMD64 model and verification scenarios, not the Sockeye framework itself.

- [Official Sockeye Website](https://sockeye.ethz.ch/)
- [Sockeye Source Repository](https://gitlab.inf.ethz.ch/project-opensockeye/sockeye)
- [AMD64 Model — Merge Request !51](https://gitlab.inf.ethz.ch/project-opensockeye/sockeye/-/merge_requests/51)

## Source Version

The model files were taken from upstream Sockeye commit:

`11473a677ce46a0671e182c6f98ed2d67ce7464f`

This snapshot incorporates changes made after the original thesis submission.

The original thesis evaluation used Sockeye version `2025-08-08+dbf0130` with the Rosette backend. Results for the later source snapshot have not been independently reverified here.

See [SOURCE_NOTES.md](SOURCE_NOTES.md) for further details.

## Related Publication

[Sockeye: Bug-finding and proofs for platform configurations and hardware based on reference manuals](https://doi.org/10.1145/3830418.3843883), ACM SOSP 2026.
