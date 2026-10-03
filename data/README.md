# Dataset setup

Source: [IBM Transactions for Anti-Money Laundering on Kaggle](https://www.kaggle.com/datasets/ealtman2019/ibm-transactions-for-anti-money-laundering-aml)

Download and extract these two files from the HI-Small subset:

- HI-Small_Trans.csv
- HI-Small_accounts.csv

Place both CSV files in this folder on the computer running the notebook:

    data/HI-Small_Trans.csv
    data/HI-Small_accounts.csv

The raw CSV files are intentionally excluded from Git. The assessment brief allows dataset download instructions when files are too large to include in the repository.

## Files used in the analysis

The notebook loads both complete HI-Small files. It does not sample the input. The query filters and analysis periods are explained in the notebook.

The local files were checked on 3 October 2026. Row counts exclude the header.

| File | Data rows | Columns |
| --- | ---: | ---: |
| `HI-Small_Trans.csv` | 5,078,345 | 11 |
| `HI-Small_accounts.csv` | 518,581 | 5 |

The Kaggle dataset version number was not recorded when these files were downloaded. The SHA-256 checksums below identify the exact file contents used:

```text
b19d39f515523373f991b689c07e11e7b0b95c17a2c27a87d91584ae16c5b040  data/HI-Small_Trans.csv
786808526e33cfc441212dd6fccda7edfc24172149bed59c6ef59b186836b014  data/HI-Small_accounts.csv
```

On macOS, check the downloaded files from the repository root with:

```sh
shasum -a 256 data/HI-Small_Trans.csv data/HI-Small_accounts.csv
```

Compare the output with the checksums above. Different file contents may produce different results.

The source dataset retains its original licence and attribution requirements; this repository does not relicense it.
