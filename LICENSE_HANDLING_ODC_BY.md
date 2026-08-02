# Agent Instructions: Handling ODC-By + Common Crawl ToU Datasets

These instructions apply to the "Generally usable with care" tier:

- FineWeb / FineWeb-Edu / FineWeb-2
- RefinedWeb
- OpenWebMath
- peS2o
- Dolma
- C4
- Most web portions of RedPajama / SlimPajama

## 1. License Classification
Treat these datasets as **ODC-By 1.0** (Open Data Commons Attribution License) **+** Common Crawl Terms of Use.
They are usable for commercial model training, but **attribution is mandatory**.

## 2. Required Attribution
Whenever you use, distribute, or publish a model trained on these datasets (or any derivative data), you must include clear attribution.

Recommended attribution text (include this in model cards, README, training logs, and DATA_ATTRIBUTION.md):

```text
This model was trained in part on data from [Dataset Name] 
(e.g. FineWeb / RefinedWeb / OpenWebMath / peS2o / Dolma / C4), 
which is released under the Open Data Commons Attribution License (ODC-By) v1.0 
and is derived from Common Crawl. 
See: https://opendatacommons.org/licenses/by/1-0/ 
and https://commoncrawl.org/terms-of-use/
```

## 3. What you can do
- Use the data for training commercial models
- Modify / filter / mix the data
- Redistribute filtered or processed versions (as long as you keep attribution)
- Create derivative datasets

## 4. What you must not do
- Remove or obscure the original license / attribution
- Claim the original data as your exclusive property
- Violate Common Crawl’s Terms of Use (especially regarding personal data and redistributing raw crawl data in ways that violate their rules)

## 5. Practical Handling Rules for the Agent

- Always keep a `source` or `license` field when converting data to JSONL/Parquet.  
  Example schema:
  ```json
  {
    "text": "...",
    "source": "fineweb",
    "license": "ODC-By-1.0 + CommonCrawl-ToU"
  }
  ```

- When creating a training mixture, maintain a simple license manifest file that lists every ODC-By dataset used and the attribution text above.

- Prefer streaming (`streaming=True`) or official sample subsets when possible to avoid unnecessary full downloads of multi-TB datasets.

- After filtering/deduplication, re-attach the license metadata so downstream users know the data origin.

## 6. Recommended Attribution File
Create a file called `DATA_ATTRIBUTION.md` (or similar) in the training repo that contains:

```markdown
## Data Attribution

The following datasets used in training are released under the 
Open Data Commons Attribution License (ODC-By) v1.0 and are derived from Common Crawl:

- FineWeb / FineWeb-Edu / FineWeb-2 (HuggingFaceFW)
- RefinedWeb (tiiuae)
- OpenWebMath
- peS2o (allenai)
- Dolma (allenai)
- C4 (allenai)
- [any others used]

Full license text: https://opendatacommons.org/licenses/by/1-0/
Common Crawl Terms of Use: https://commoncrawl.org/terms-of-use/
```

## 7. Summary Rule for the Agent
> “These datasets are commercially usable. Always keep attribution. Never strip the license information. Prefer keeping a `source` + `license` field in every processed example.”

These instructions are recorded here so the agent stays consistent and does not drift.
