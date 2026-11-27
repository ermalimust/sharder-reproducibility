# Sharder reproducibility materials

Reproducibility materials for **Where Cross-Shard Coordination Becomes a Bottleneck: Cost Decomposition and a Coordination-Lock-Free Architecture for Sharded Blockchains**.

## Download and start

Download the two named assets from [release v1.1.0 (R2)](https://github.com/ermalimust/sharder-reproducibility/releases/tag/v1.1.0).

| Asset | Contents and starting point |
| --- | --- |
| `FGCS_reproducibility_public_v1.0.0.zip` | Original simulator, emulator, configurations, per-seed results, figures and tests. Extract the archive and open `artifact/README.md`. The same archive is available in [v1.0.0](https://github.com/ermalimust/sharder-reproducibility/releases/tag/v1.0.0). |
| `FGCS_R2_evidence.zip` | Paired DES data for 20 seeds, replay and analysis scripts, Ed25519 benchmark and batch timings, and aggregate results for the 365-transaction persistence replay. Extract this archive separately and open its top-level `README.md`. |

From the extracted R2 companion, run `python paired_des/recompute.py` to reproduce the latency comparison and paired 95% confidence interval. For the 365-transaction replay, only aggregate results are available. The original input trace and per-transaction timings are unavailable.

In the original package's `artifact/` directory:

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
