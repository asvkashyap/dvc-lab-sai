\# DVC Lab: Data Versioning with Google Cloud Storage



Completed version of the DADS 7305 DVC lab (Labs/Data\_Labs/DVC\_Labs/Lab\_1), using DVC with a GCS bucket as remote storage.



\## Modifications from the original lab

\- \*\*Dataset:\*\* California Housing (scikit-learn) instead of CC\_GENERAL.csv

\- \*\*Second data version:\*\* v2 removes rows where `MedHouseVal` is capped at the dataset ceiling (20,640 rows to 19,648)

\- \*\*Revert demonstrated:\*\* restored v1 from Git history with `dvc checkout`, verified by row count

\- \*\*Least privilege:\*\* service account uses Storage Object Admin instead of Owner

\- \*\*Credentials kept local:\*\* key path stored with `dvc remote modify --local`, so it is never committed



\## Data versions

| Version | Commit | Rows | Description |

|---|---|---|---|

| v1 | 36fec8b | 20,640 | Raw California Housing data |

| v2 | 1a97c47 | 19,648 | Capped `MedHouseVal` rows removed |



\## Setup

```

python -m venv .venv

.venv\\Scripts\\activate

pip install -r requirements.txt

dvc remote modify --local myremote credentialpath <path-to-your-key.json>

dvc pull

```

`dvc pull` requires access to the GCS bucket.



\## Switching versions

```

git checkout 36fec8b data/housing.csv.dvc

dvc checkout

```

Use `git checkout main data/housing.csv.dvc` followed by `dvc checkout` to return to the latest version.

