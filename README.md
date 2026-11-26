# Formal Verification of the FRI-Binius Protocol in ArkLib

[Preprint releases](https://github.com/chung-thai-nguyen/fri-binius-fv/releases) · [Browse the Lean formalization](https://github.com/chung-thai-nguyen/ArkLib/tree/main/ArkLib/ProofSystem/Binius) · [Reproduce the checks](REPRODUCE.md)

This project verifies the oracle protocols underlying FRI-Binius in Lean 4: Binary BaseFold, ring switching, and their modular and unrolled compositions. The security proof bounds the probability of a new bad folding event at each verifier challenge. For unrolled FRI-Binius, we derive ordinary knowledge soundness and soundness with the same aggregate error bound as the round-by-round analysis.

The proofs concern the interactive oracle protocol. They do not verify its cryptographic compilation or a production implementation.

No preprint has been released from this repository yet. Each release will pair the PDF with its exact ArkLib revision, a table linking statements in the paper to Lean declarations, and instructions for checking the results.
