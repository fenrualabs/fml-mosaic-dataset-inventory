# AGENT START PLAN – FML-Mosaic-527B High Quality Mixture

**This is the authoritative plan for the agent.**  
Follow this file step by step.

**Hardware constraints:**
- Remote storage available: 11.2 TB
- Local training disk: 5 TB
- Internet: ~950 MB/s
- Existing data: ~25 GB of text JSONs

**Target:** Highest quality practical mixture (aim for 7–10 TB total)

---

## 1. Directory Structure (Create First)

```bash
/data/
  raw/
  filtered/
  jsonl/
    existing/          # put your current 25 GB here
    phase1/
    phase2/
    phase3/
  mixtures/
  attribution/
  logs/
```

---

## 2. Required JSONL Schema

Every example must follow this format:

```json
{
  "text": "the actual text content",
  "source": "openwebmath | fineweb-edu | pes2o | stack-v2 | gutenberg | etc",
  "license": "ODC-By-1.0 + CommonCrawl-ToU | MIT | Apache-2.0 | Public Domain | CC-BY-4.0 | NVIDIA"
}
```

Always keep the `source` and `license` fields. See `LICENSE_HANDLING_ODC_BY.md`.

---

## 3. Priority Download & Processing Order

### Phase 1 – Immediate High-Signal (Start Now)
These are smaller, extremely high quality, and give you usable data quickly:

| Order | Dataset | Hugging Face ID | Approx Size | License |
|-------|---------|------------------|-------------|--------|
| 1 | OpenWebMath | `open-web-math/open-web-math` | 40–55 GB | ODC-By |
| 2 | OpenMathInstruct-1 | `nvidia/OpenMathInstruct-1` | ~9 GB | NVIDIA (commercial OK) |
| 3 | OpenMathInstruct-2 | `nvidia/OpenMathInstruct-2` | ~13 GB | CC-BY-4.0 |
| 4 | Project Gutenberg | `manu/project_gutenberg` | ~14 GB | Public Domain |
| 5 | UltraChat 200k | `HuggingFaceH4/ultrachat_200k` | 1.6 GB | MIT |
| 6 | OASST1 | `OpenAssistant/oasst1` | < 1 GB | Apache-2.0 |
| 7 | OpenOrca | `Open-Orca/OpenOrca` | several GB | MIT |

**Action:** Download → convert to the JSONL schema → put in `/data/jsonl/phase1/`

### Phase 2 – Core Knowledge (Highest Priority Large Sets)

| Order | Dataset | Hugging Face ID | Target Size | License |
|-------|---------|------------------|-------------|--------|
| 1 | peS2o | `allenai/peS2o` | ~308 GB | ODC-By |
| 2 | FineWeb-Edu | `HuggingFaceFW/fineweb-edu` | 1.5 – 2.5 TB | ODC-By |
| 3 | Common Pile (filtered components first) | See `COMMON_PILE_COMPONENTS.md` | 1.5 – 2.5 TB | PD / Open |

Start with the highest value Common Pile components (arXiv, books, educational, scientific).

### Phase 3 – Code + Additional Web

| Dataset | Hugging Face ID | Target Size after filtering | Notes |
|---------|------------------|-----------------------------|-------|
| The Stack v2 | `bigcode/the-stack-v2` | 1.5 – 2.5 TB | **Heavily filter** – do not take full size |
| FineWeb (selected) | `HuggingFaceFW/fineweb` | 0.5 – 1.5 TB | Prefer sample-350BT or high-quality dumps |

### Phase 4 – Additional SFT (keep relatively small)

- Selected NVIDIA Nemotron SFT sets (Math, SWE, Science, Instruction)
- Put in `/data/jsonl/phase1/` or a dedicated SFT folder

---

## 4. How the Agent Should Work

1. Always process one dataset at a time.
2. Prefer **streaming** for large datasets (`streaming=True`).
3. Apply quality filters while streaming when possible.
4. Write clean JSONL files with the required schema.
5. Update a running attribution / license manifest.
6. After Phase 1 + peS2o + FineWeb-Edu are ready, you already have a strong core mixture and can start experimental training runs.
7. Use the 5 TB local disk only for active shuffled training batches. Keep the full store on the 11.2 TB remote.

---

## 5. Success Criteria

- Total high-quality data between 7–10 TB
- All examples carry `source` + `license` fields
- Existing 25 GB JSONs are preserved and can be mixed in
- Clear DATA_ATTRIBUTION.md is maintained
- Phase 1 completed first so training can start early

---

## 6. Reference Files in This Repo

- `DATASET_INVENTORY.md` → full list of safe datasets
- `COMMON_PILE_COMPONENTS.md` → breakdown of Common Pile sources
- `LICENSE_HANDLING_ODC_BY.md` → how to handle ODC-By datasets
- `ACCESS_AND_CONVERSION_NOTES.md` → conversion tips
- `RECOMMENDED_MIXTURE_PLAN.md` → high-level overview

**This AGENT_START_PLAN.md is the operational plan. Follow it.**
