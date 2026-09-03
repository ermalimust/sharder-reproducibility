# Sharder reproducibility materials

Reproducibility materials for **Where Cross-Shard Coordination Becomes a Bottleneck: Cost Decomposition and a Coordination-Lock-Free Architecture for Sharded Blockchains**.

## Download and start

Open this repository's **Releases** tab, select **v1.0.0**, and download the named asset **`FGCS_reproducibility_public_v1.0.0.zip`**. This release package contains the complete source code, configurations, raw data, aggregate results, figures, and validation materials. Use this named asset for reproduction, rather than GitHub's automatically generated source archives.

Extract the ZIP and open its `artifact/` directory:

- `README.md` provides the study commands, environment information, and measurement definitions.
- `EVIDENCE_MAP.md` connects each study to its data, figures, and validation checks.
- `manifest.json` records file sizes and SHA-256 checksums for package integrity.

## Quick verification

The package has been verified with **Python 3.14.5**. Its requirements are `numpy==2.5.1`, `matplotlib==3.11.1`, and `simpy>=4.1,<5`; install them using the included requirements file.

Run the following commands **from the extracted `artifact/` directory**. They create a virtual environment beside the artifact and run the **82-test** suite, including package-integrity verification.

### PowerShell

```powershell
py -3.14 -m venv ..\fgcs_artifact_venv
& ..\fgcs_artifact_venv\Scripts\python.exe -m pip install -r 03_experiments\code\requirements.txt
& ..\fgcs_artifact_venv\Scripts\python.exe -B -m unittest discover -s 03_experiments\tests -p "test_*.py"
```

### POSIX shell

```sh
python3.14 -m venv ../fgcs_artifact_venv
../fgcs_artifact_venv/bin/python -m pip install -r 03_experiments/code/requirements.txt
../fgcs_artifact_venv/bin/python -B -m unittest discover -s 03_experiments/tests -p "test_*.py"
```

A successful check reports `Ran 82 tests` and `OK`. Run this check before generating new reproduction outputs: the integrity test verifies the packaged file set as well as its checksums. Then follow the package's `README.md` for the full study commands.

## What the evidence covers

The discrete-event simulation compares four cross-shard coordination families under explicitly defined resource budgets. The single-host threaded emulator exercises protocol and recovery paths and reports runtime resources. It executes SHA-256 Merkle-tree construction and verification; certificate authentication uses deterministic test substitutes. Read the package's measurement definitions when interpreting each result.
