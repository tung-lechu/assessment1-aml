# Assessment 1 Historical AML Analysis with Apache Spark

Student ID: 33602190  
Unit code: To be completed  
Semester: To be completed  
Year: 2026

## Progress

Phase 1 proposal approval has been confirmed by the student. Step 1 provides a runnable Spark environment and notebook setup check. Dataset loading and analytical implementation are the next milestones; no AML findings are claimed yet.

## Files

- `assessment1.ipynb`: main notebook with saved setup outputs; later milestones will add Parts A and B.
- `requirements.txt`: pinned direct Python dependencies.
- `requirements-lock.txt`: full resolved Python environment from the verified setup.
- `data/README.md`: source and local dataset placement instructions.
- `.vscode/`: Python interpreter preference and recommended extensions.

The approved `proposal/proposal.md` and Part B DAG screenshot will be added in later milestones.

## Reproduce the environment

Use Python 3.11, Java 17 and Spark 3.5.7. Spark's [installation documentation](https://spark.apache.org/docs/3.5.7/api/python/getting_started/install.html) describes supported versions. This setup uses local Spark, not a remote cluster.

### Python environment

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) if unavailable. On this Mac, uv is installed through Homebrew. From the repository root:

```sh
uv python install 3.11.17
uv venv --python 3.11.17 --managed-python .venv
uv pip install --python .venv/bin/python -r requirements-lock.txt
.venv/bin/python -m ipykernel install --user --name assessment1-aml --display-name "Python (assessment1-aml)"
```

The initial environment was resolved from `requirements.txt`; use the lock file to reproduce the tested versions. On Windows, use `.venv\Scripts\python.exe` instead of `.venv/bin/python`.

### Java

Install a Java 17 JDK for your operating system from [Eclipse Adoptium](https://adoptium.net/temurin/releases/?version=17), and set `JAVA_HOME` to its installation directory if necessary.

On this Apple Silicon Mac, the verified project-local runtime is Temurin 17.0.20.1+1 in `.runtime/jdk-17.0.20.1+1/Contents/Home`. It was downloaded from the official Adoptium release and checked against the publisher's SHA-256 checksum. The notebook discovers this location automatically. The runtime is not committed to Git.

A project-local copy on another Apple Silicon Mac can be prepared with:

```sh
mkdir -p .runtime
curl -fL 'https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.20.1%2B1/OpenJDK17U-jdk_aarch64_mac_hotspot_17.0.20.1_1.tar.gz' -o .runtime/java17.tar.gz
echo '196d13ba5f10414bef7f6a05a9b3f00edacb18ebacef2b99485db9e2ee18f0e8  .runtime/java17.tar.gz' | shasum -a 256 -c -
# Continue only if the checksum reports OK.
tar -xzf .runtime/java17.tar.gz -C .runtime
```

Setup note: Homebrew Java installation encountered an existing freetype directory conflict, and Homebrew Python returned an empty macOS version. The working setup therefore uses the project-local Temurin runtime and uv-managed Python. No global shell profile edits are required.

### Open and run

1. Follow `data/README.md` to place both CSV files in `data/`.
2. Open this repository folder in VS Code.
3. Enable the Microsoft Python and Jupyter extensions, if prompted.
4. Open `assessment1.ipynb` and select **Python (assessment1-aml)** or the repository's `.venv` interpreter.
5. Use **Restart Kernel and Run All**. The setup check must report count 10 and sum 45, find both input files, and stop Spark cleanly.

Alternatively, launch JupyterLab from the repository root:

```sh
.venv/bin/jupyter lab
```

To rerun and save all outputs from the terminal:

```sh
.venv/bin/jupyter nbconvert --execute --to notebook --inplace assessment1.ipynb --ExecutePreprocessor.timeout=180
```

## Initial Spark settings

- Execution: `local[4]`, up to four task threads on one computer.
- Driver heap: 4 GB; actual JVM maximum heap is displayed in the notebook.
- Executor memory configuration: 4 GB; local mode has no separate remote executor heaps.
- Shuffle partitions: 8, provisional until the Part B experiments.
- Adaptive query execution: enabled.
- Session timezone: UTC, a parsing convention rather than a claim about the dataset's timezone.

The notebook reports the actual Python, Java, Spark, OS and available CPU details. Restart the kernel before changing JVM memory settings. The final setup cell stops Spark; future analytical cells should precede that cleanup. Capture the Spark Web UI evidence in Part B before stopping the session.

## Development and AI assistance

Keep genuine milestone commits as work progresses. OpenAI Codex assisted with repository setup, environment troubleshooting, documentation and the Step 1 notebook. The student must understand and verify submitted code, maintain an AI acknowledgement, and write discussion based on genuine engagement with observed results.

## Marking access

If this repository is private, grant the tutor or unit organisation access before submission. Raw datasets and local runtimes are excluded from Git.
