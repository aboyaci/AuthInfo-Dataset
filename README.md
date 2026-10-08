# AuthInfo-Dataset

Username–password pairs drawn from eight leaked online-service breaches, with per-password structural features. Usernames are anonymized; passwords are kept as-is so their composition can be studied.

This is the dataset behind:

> E. Y. Güven, **A. Boyacı**, M. A. Aydın. *A novel password policy focusing on altering user password selection habits: A statistical analysis on breached data.* **Computers & Security**, vol. 113, 102560, 2022. [doi:10.1016/j.cose.2021.102560](https://doi.org/10.1016/j.cose.2021.102560)

The paper analyzes more than ten million pairs to find which composition habits actually make passwords guessable. It then proposes a behavior-based policy aimed at those habits, rather than generic "one uppercase, one digit" rules.

## What's here

| Path | Contents |
|---|---|
| `AuthInfo-Dataset.csv` | A **5-row sample** showing the format |
| `figures/` | Data-gathering workflow diagram |
| [Full dataset (Google Drive)](https://drive.google.com/drive/folders/1ufsv8_PMTT36h3M5rXjKRr8P6BauYkDN?usp=sharing) | The complete data used in the paper |

## Schema

| Column | Meaning | Example |
|---|---|---|
| `id` | Row number | `1` |
| `username` | Salted hash of the original username (32 hex chars) | `6dd3122b97…` |
| `password` | Password as leaked | `hamoo4248423` |
| `lenght` | Password length *(column name typo kept for compatibility)* | `12` |
| `typeofchar` | Character classes present: `l` lower, `u` upper, `d` digit, `s` special | `dl` |
| `source` | Breach the pair came from | `Crossfire.txt` |
| `firstchar` | Class of the first character | `l` |
| `countl` / `countu` / `countd` / `counts` | Count of lower / upper / digit / special characters | `5` / `0` / `7` / `0` |
| `mask` | Password with each character replaced by its class | `lllllddddddd` |

## Loading it

```python
import pandas as pd

df = pd.read_csv("AuthInfo-Dataset.csv", skipinitialspace=True)
df.groupby("typeofchar")["lenght"].describe()
```

## Ethics & use

Every password here was already public through breaches. Usernames are hashed to break the link to individuals. Use the data for research on password security and policy, and don't attempt to re-identify users.

## Citation

```bibtex
@article{guven2022novel,
  title   = {A novel password policy focusing on altering user password selection habits: A statistical analysis on breached data},
  author  = {G{\"u}ven, Ebu Yusuf and Boyac{\i}, Ali and Ayd{\i}n, Muhammed Ali},
  journal = {Computers \& Security},
  volume  = {113},
  pages   = {102560},
  year    = {2022},
  doi     = {10.1016/j.cose.2021.102560}
}
```

Originally published by [istec-iuc](https://github.com/istec-iuc/AuthInfo-Dataset).
