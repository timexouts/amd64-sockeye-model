
# Source Notes

## Model Source

The six files in `model/` were taken from the AMD64 specification directory of the upstream Sockeye repository:

https://gitlab.inf.ethz.ch/project-opensockeye/sockeye

Source commit:

`11473a677ce46a0671e182c6f98ed2d67ce7464f`

Merge Request:

https://gitlab.inf.ethz.ch/project-opensockeye/sockeye/-/merge_requests/51

The model files were copied without modification.

## Thesis Version

The bachelor's thesis was completed in August 2025.

The evaluation was performed using Sockeye version `2025-08-08+dbf0130` with the Rosette backend.

The code included in this repository is a later upstream snapshot and should not be treated as identical to the original thesis submission.

## Verification

The thesis reported:

- Reproduction of the Sinkclose vulnerability in the AMD64 model
- A modeled mitigation preventing the attack
- Inductive verification of user-mode isolation properties

These results depend on the specified model and assumptions.

The scenarios have not yet been rerun using this standalone repository.

## Attribution

The AMD64 model was developed as part of a bachelor's thesis at ETH Zürich, with subsequent improvements contributed to the upstream Sockeye project.

Sockeye itself is a separate research project developed by the ETH Zürich research team.

The upstream development history should be consulted for individual contributions and authorship.

## Reproducibility

For reproduction of the original thesis results, use the thesis-tested model and compatible Sockeye version.

The updated files in this repository may require a different framework revision.

## Redistribution

Before public release, confirm permission to redistribute the model files and thesis PDF, and verify the applicable upstream licensing and contributor attribution.
