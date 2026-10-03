# Assessment 1 Historical AML Analysis with Apache Spark

Student ID: 33602190
Unit code: ITO5202
Semester: Spring Semester
Year: 2026

## Dataset

IBM Transactions for Anti-Money Laundering, HI-Small subset. See [data/README.md](data/README.md) for the source and download instructions.

## Reproduce the environment

Use Python 3.11, Java 17 and Spark 3.5.7. Spark's [installation documentation](https://spark.apache.org/docs/3.5.7/api/python/getting_started/install.html) describes supported versions. This setup uses local Spark, not a remote cluster.

### Python environment

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) if unavailable. On this Mac, uv is installed through Homebrew. From the repository root:

```sh
uv python install 3.11.17
uv venv --python 3.11.17 --managed-python .venv
uv pip install --python .venv/bin/python -r requirements.txt
```

The direct dependencies are pinned in `requirements.txt`. Transitive dependency versions may vary between installations. On Windows, use `.venv\Scripts\python.exe` instead of `.venv/bin/python`.

### Java

Install a Java 17 JDK for your operating system from [Eclipse Adoptium](https://adoptium.net/temurin/releases/?version=17), and set `JAVA_HOME` to its installation directory if necessary.

On this Apple Silicon Mac, the verified runtime stored in this project is Temurin 17.0.20.1+1 in `.runtime/jdk-17.0.20.1+1/Contents/Home`. It was downloaded from the official Adoptium release and checked against the publisher's SHA-256 checksum. The kernel registration below configures this location. The runtime is not committed to Git.

To install a copy inside this project on another Apple Silicon Mac, run:

```sh
mkdir -p .runtime
curl -fL 'https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.20.1%2B1/OpenJDK17U-jdk_aarch64_mac_hotspot_17.0.20.1_1.tar.gz' -o .runtime/java17.tar.gz
echo '196d13ba5f10414bef7f6a05a9b3f00edacb18ebacef2b99485db9e2ee18f0e8  .runtime/java17.tar.gz' | shasum -a 256 -c -
# Continue only if the checksum reports OK.
tar -xzf .runtime/java17.tar.gz -C .runtime
```

### Register the notebook kernel

After installing Python dependencies and Java, register the kernel. On this Mac, run these commands from the repository root. On another machine, replace the Java path with your Java 17 installation directory.

```sh
.venv/bin/python -m ipykernel install --user \
  --name assessment1-aml --display-name "Python (assessment1-aml)" \
  --env JAVA_HOME "$PWD/.runtime/jdk-17.0.20.1+1/Contents/Home" \
  --env PYSPARK_PYTHON "$PWD/.venv/bin/python" \
  --env SPARK_LOCAL_IP 127.0.0.1 \
  --env PYSPARK_SUBMIT_ARGS "--driver-memory 4g pyspark-shell"
```

This keeps configuration specific to your computer outside the notebook. Register the kernel again if the project folder moves. Restart the notebook kernel after changing its configuration.

### Open and run

1. Follow `data/README.md` to place both CSV files in `data/`.
2. Open this repository folder in VS Code.
3. Enable the Microsoft Python and Jupyter extensions, if prompted.
4. Open `assessment1.ipynb` and select **Python (assessment1-aml)** from the registered Jupyter kernels (not a generic Python environment).
5. Use **Restart Kernel and Run All**.

