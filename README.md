# BLB / CKKS-MPC Zenodo v1 mirror

## Repository provenance

This repository is a GitHub mirror of the authors' **Zenodo v1 source artifact** for the paper **"Breaking the Layer Barrier: Remodeling Private Transformer Inference with Hybrid CKKS and MPC"**.

The repository owner downloaded `CKKS-MPC-main.zip` from the authors' Zenodo v1 release and uploaded its contents here for easier source inspection and experiment reproduction. Treat this repository as a convenience mirror of that artifact, **not as an independent upstream release or a separately maintained fork**.

Canonical artifact records:

- Zenodo v1 source artifact: https://zenodo.org/records/15590214
- Later Zenodo v3 supplemental record: https://zenodo.org/records/15627952

## Relationship to the author Docker source

The companion private repository `best-orange/blbv1-source-snapshot` contains a byte-verified extraction from the authors' pinned `blbv1` Docker image:

```text
image digest:
sha256:f696ecc441daeb1e05daaee6b955e12cdc5ea0cbb1f5335dab57f769167d20b4

CKKS-MPC HEAD:
cfd3884869c64fb8c5259a4e012d1b4ea746741e
```

A complete path/content comparison has been performed between this Zenodo v1 mirror and the Docker full-source archive. The common CKKS/MPC/BERT bridge source has no semantic divergence: raw-byte differences on common source paths are line-ending differences except for the root README setup notes. In particular, the bridge focal files such as `fixed-point.cpp`, `ckks_bert.cpp`, `linear_ckks.cpp`, `he.cpp`, and `nonlinear.cpp` match semantically, with the major focal files byte-identical.

The Docker archive additionally contains dependency source bodies that are not present in Zenodo v1, notably the complete vendored SEAL and Phantom source trees.

The Zenodo v3 `0001-more-flexible.patch` is a later Phantom supplement. It is preserved separately in `best-orange/blbv1-source-snapshot/upstream-artifact/zenodo-v3/` and was verified **not to be applied** in the pinned `blbv1` Docker Phantom source.

## Repository roles

```text
best-orange/blb
= authors' Zenodo v1 source artifact mirrored on GitHub

best-orange/blbv1-source-snapshot
= byte-verified source from the pinned author blbv1 Docker image
  + provenance/diff evidence
  + separately preserved Zenodo v3 supplement

best-orange/he_sa
= our UNet hybrid CKKS+MPC research, diagnostics, repairs, and experiments
```

Do not interpret experimental fixes in `he_sa` as changes to the original Zenodo artifact or to the preserved Docker source.

---

## Original artifact README

This is the official implementation of the paper "Breaking the Layer Barrier: Remodeling Private Transformer Inference with Hybrid CKKS and MPC".

## Setup
```
./setup_env_and_build.sh
clone phantom from https://github.com/encryptorion-lab/phantom-fhe.git
apply 0001-.patch for phantom
build phantom in SCI/extern/phantom
```

## Build
```
cd SCI/tests
mkdir build && cd build
cmake -DCMAKE_INSTALL_PREFIX=./install .. -DNO_REVEAL_OUTPUT=ON
cmake --build . --target install --parallel
```
## Run
```
./bin/ckks_bert_large_main r=1 p=1234 && ./bin/ckks_bert_large_main ip=127.0.0.1 r=2 p=1234
```
## Test data
Important test data in BLB paper is in `/SCI/output/`
