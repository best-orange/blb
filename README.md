# BLB / CKKS-MPC artifact mirror

## Repository provenance

This GitHub repository is a convenience mirror of the source artifact downloaded from the authors' **Zenodo v1 release** for the paper **"Breaking the Layer Barrier: Remodeling Private Transformer Inference with Hybrid CKKS and MPC"**. The repository owner downloaded the v1 artifact (`CKKS-MPC-main.zip`) from Zenodo and uploaded its contents here for easier source inspection and experiment reproduction.

This repository should therefore be treated as a mirror of the authors' Zenodo v1 artifact, **not as an independent upstream release or a separately maintained fork**.

Canonical artifact records:

- Zenodo v1 source artifact: https://zenodo.org/records/15590214
- Later Zenodo record / artifact update: https://zenodo.org/records/15627952

For provenance-sensitive experiments, distinguish the following artifacts:

1. `best-orange/blb`: mirror of the authors' Zenodo v1 source artifact;
2. `best-orange/blbv1-source-snapshot`: byte-verifiable source snapshot extracted from the authors' `blbv1` Docker image actually used for reproduction;
3. `best-orange/he_sa`: our research repository containing diagnostic patches, validation experiments, and HE/MPC work for private UNet inference.

Do not interpret experimental fixes in `he_sa` as changes to the original Zenodo artifact.

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

