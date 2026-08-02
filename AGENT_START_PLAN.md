# AGENT START PLAN – FML-Mosaic-527B (Precise Version)

**This is the single source of truth for the agent.**  
Follow this document exactly. Do not improvise or change priorities unless explicitly instructed.

**Hardware constraints (do not exceed):**
- Remote storage: 11.2 TB available
- Local training disk: 5 TB
- Internet: ~950 MB/s
- Existing data: ~25 GB of text JSONs (preserve them)

**Goal:** Build the highest quality practical mixture that fits under 11 TB.

---

## 0. Authentication (Mandatory)

You **must** use the Hugging Face access token that has been provided to you.

- Log in with the token before any download:
  ```bash
  huggingface-cli login --token $HF_TOKEN
  ```
  or set the environment variable `HF_TOKEN` and use the `huggingface_hub` library.

- Prefer **public** datasets only. Do not try to access gated or private datasets unless the token specifically grants access and the plan explicitly includes them.

- Always work with the public Hugging Face Hub datasets listed in this plan.

---

## 1. Directory Structure (Create First)

```bash
mkdir -p /data/{raw,filtered,jsonl/{existing,phase1,phase2,phase3,sft},mixtures,attribution,logs}
```

- Put the existing ~25 GB of JSONs into `/data/jsonl/existing/`
- Never overwrite existing data

---

## 2. Mandatory JSONL Schema

Every single example you write must use this exact schema:

```json
{
  "text": "the actual text content here",
  "source": "openwebmath",
  "license": "ODC-By-1.0 + CommonCrawl-ToU"
}
```

Allowed `license` values (use the correct one):
- `ODC-By-1.0 + CommonCrawl-ToU`
- `Public Domain`
- `MIT`
- `Apache-2.0`
- `CC-BY-4.0`
- `NVIDIA`
- `PD / Open`

See `LICENSE_HANDLING_ODC_BY.md` for attribution rules.

---

## 3. Execution Order (Follow Strictly)

### Phase 1 – High-Signal Small Datasets (Start Immediately)

Download and convert these first. They are small and high quality.

| Priority | Dataset                    | Exact Hugging Face ID                  | Target Size | License                          |
|----------|----------------------------|----------------------------------------|-------------|----------------------------------|
| 1        | OpenWebMath                | `open-web-math/open-web-math`          | ~27–55 GB  | ODC-By-1.0 + CommonCrawl-ToU    |
| 2        | OpenMathInstruct-1         | `nvidia/OpenMathInstruct-1`            | ~9 GB      | NVIDIA                          |
| 3        | OpenMathInstruct-2         | `nvidia/OpenMathInstruct-2`            | ~13 GB     | CC-BY-4.0                       |
| 4        | Project Gutenberg          | `manu/project_gutenberg`               | ~14 GB     | Public Domain                   |
| 5        | UltraChat 200k             | `HuggingFaceH4/ultrachat_200k`         | ~1.6 GB    | MIT                             |
| 6        | OASST1                     | `OpenAssistant/oasst1`                 | < 1 GB     | Apache-2.0                      |
| 7        | OpenOrca                   | `Open-Orca/OpenOrca`                   | several GB | MIT                             |

**Instructions for Phase 1:**
1. Use `datasets` library or `huggingface-cli` with the token.
2. Convert every example to the mandatory JSONL schema.
3. Save into `/data/jsonl/phase1/`
4. Log progress in `/data/logs/`

### Phase 2 – Core Knowledge (Highest Priority Large Sets)

| Priority | Dataset              | Exact Hugging Face ID              | Target Size     | License                       |
|----------|----------------------|------------------------------------|-----------------|-------------------------------|
| 1        | peS2o (prefer V2)    | `allenai/peS2o`                    | ~308 GB        | ODC-By-1.0                   |
| 2        | FineWeb-Edu          | `HuggingFaceFW/fineweb-edu`        | 1.5 – 2.5 TB   | ODC-By-1.0 + CommonCrawl-ToU |
| 3        | Common Pile Filtered | See `COMMON_PILE_COMPONENTS.md`    | 1.5 – 2.5 TB   | PD / Open                    |

**FineWeb-Edu instructions:**
- Prefer starting with the official samples: `sample-10BT`, `sample-100BT`, then `sample-350BT`
- Then move to individual high-quality dumps or the full set if space remains
- Always use `streaming=True` when possible and write filtered JSONL on the fly

**Common Pile instructions:**
- Start with the highest value components first (arXiv, books, educational, scientific, StackExchange)
- Use the filtered collection when available

### Phase 3 – Code + Additional Web

| Dataset          | Exact Hugging Face ID             | Target Size after filtering | Notes |
|------------------|-----------------------------------|-----------------------------|-------|
| The Stack v2     | `bigcode/the-stack-v2` (prefer train-smol or selected languages) | 1.5 – 2.5 TB | Heavily filter. Do not download the full 32 TB deduped version. |
| FineWeb          | `HuggingFaceFW/fineweb`           | 0.5 – 1.5 TB               | Only after Phase 2 is well underway. Prefer sample-350BT. |

### Phase 4 – Additional SFT (Keep Small)

Only after Phase 1–3 are progressing well:
- Selected public NVIDIA Nemotron SFT datasets (Math, Science, Instruction, SWE)
- Put them in `/data/jsonl/sft/`

---

## 4. Strict Rules for the Agent (Do Not Drift)

1. Follow the priority order above. Do not jump ahead.
2. Always authenticate with the Hugging Face token first.
3. Prefer public datasets listed in this plan.
4. Use streaming for any dataset larger than ~100 GB.
5. Always write the mandatory JSONL schema with `text`, `source`, and `license`.
6. Keep a running attribution file in `/data/attribution/`.
7. Never delete or overwrite the existing 25 GB of data.
8. Leave at least 1 TB free on the 11.2 TB storage as buffer.
9. Use the 5 TB local disk only for active training mixtures.
10. Log every major action.

---

## 5. Reference Files (Read Them)

- `DATASET_INVENTORY.md` – full safe dataset list
- `COMMON_PILE_COMPONENTS.md` – Common Pile source breakdown
- `LICENSE_HANDLING_ODC_BY.md` – how to handle ODC-By datasets
- `ACCESS_AND_CONVERSION_NOTES.md` – conversion tips

---

**This document is the operational plan.**  
Execute it in order. Do not invent new datasets or change the priority without explicit instruction.
