# Reproduce the Lean checks

Use the files attached to the **same** [release](https://github.com/chung-thai-nguyen/fri-binius-fv/releases) as the PDF you are reading. The `main` branch of ArkLib is useful for browsing, but it is not the paper's reproducibility target.

1. Verify the downloaded files from the download directory with `shasum -a 256 -c SHA256SUMS` (or `sha256sum -c SHA256SUMS` on Linux).
2. Read the repository URL and full commit SHA from `arklib-pin.json`. `paper-lean-map.json` gives the pinned source link for each mapped statement; Appendix C of the paper provides a human-readable index.
3. With Git, Bash, Elan, `uv`, and Python 3.12 installed, run the commands below from the download directory. Elan selects the Lean version recorded by the checked-out `lean-toolchain` file. The first build downloads dependencies.

```bash
set -euo pipefail
pin=$(pwd -P)/arklib-pin.json
repo=$(python3.12 -c 'import json, sys; print(json.load(open(sys.argv[1]))["repository"])' "$pin")
commit=$(python3.12 -c 'import json, sys; print(json.load(open(sys.argv[1]))["commit"])' "$pin")
run=$(mktemp -d)
git clone "$repo" "$run/ArkLib"
cd "$run/ArkLib"
git checkout --detach "$commit"
lake exe cache get
git -C .lake/packages/VCVio submodule update --init --recursive
./scripts/validate.sh --axioms --docs
lake exe axiomsweep --out "$run/axiom-dependencies.json"
printf 'Axiom report: %s\n' "$run/axiom-dependencies.json"
```

The validation script builds ArkLib, runs its tests, checks axioms and admissions, and builds the Lean documentation. The axiom report records dependencies; it is not a runtime benchmark or a test of a production Binius implementation. There is no local patch to apply to the pinned source.
