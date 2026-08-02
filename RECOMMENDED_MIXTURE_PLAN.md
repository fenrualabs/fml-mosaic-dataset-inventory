# Recommended High-Quality Mixture Plan for FML-Mosaic-527B

**Storage constraints**  
- Remote: 11.2 TB available  
- Local disk for training batches: 5 TB  
- Internet: 950 MB/s  
- Existing data: ~25 GB of text JSONs

**Goal**  
Build the highest-quality practical mixture that fits comfortably under 11 TB while providing strong data for a 527B model.

---

## Target Mixture (High Quality Focus)

| Priority | Source                              | Target Size     | Notes |
|---------|-------------------------------------|------------------|-------|
| 1       | Common Pile v0.1 (filtered preferred) | 1.5 – 3 TB      | Cleanest large open data |
| 2       | FineWeb-Edu                         | 1.5 – 2.5 TB     | Highest educational quality |
| 3       | FineWeb (selected high-quality dumps or sample-350BT) | 0.5 – 1.5 TB | Strong general web |
| 4       | peS2o                               | ~300 GB          | High-quality scientific papers |
| 5       | OpenWebMath                         | ~40–55 GB        | Best open math web data |
| 6       | The Stack v2 (heavily filtered)     | 1.5 – 2.5 TB     | Best permissive code |
| 7       | Project Gutenberg + Common Pile books | 50–150 GB      | Clean long-form text |
| 8       | OpenMathInstruct-1 + OpenMathInstruct-2 | ~20–25 GB    | Strong math instruction data |
| 9       | UltraChat 200k + OASST1 + OpenOrca + selected Nemotron SFT | 30–80 GB | High-signal conversational / SFT |

**Total target**: 7 – 10 TB of high-quality data

---

## Realistic Step-by-Step Starting Plan

### Phase 0 – Preparation
1. Create a working directory structure on remote storage:
   ```
   /data/
     raw/
     filtered/
     jsonl/
     mixtures/
     attribution/
   ```
2. Keep your existing ~25 GB of JSONs in `/data/jsonl/existing/`.
3. Always maintain license metadata (`source` + `license` fields) as defined in `LICENSE_HANDLING_ODC_BY.md`.

### Phase 1 – Start with the Cleanest & Highest Signal (Week 1)
Download and convert these first (high quality, manageable size):

1. **OpenWebMath** (~40–55 GB)
2. **OpenMathInstruct-1 + OpenMathInstruct-2** (~20–25 GB)
3. **Project Gutenberg** (~14 GB)
4. **UltraChat 200k + OASST1 + OpenOrca** (~5–8 GB)
5. Selected **Nemotron SFT** sets you want (math / code / instruction)

Convert everything to consistent JSONL format with `text`, `source`, and `license` fields.

These give you immediate high-quality math + books + instruction data while the larger downloads run.

### Phase 2 – Core Knowledge & Scientific (Priority)
1. Download **peS2o** (~308 GB) — excellent scientific signal.
2. Start downloading **FineWeb-Edu** (aim for 1.5–2.5 TB).
3. Begin **Common Pile** filtered components (prioritize arXiv, books, StackExchange, educational sources first).

Use streaming where possible and write filtered examples directly to JSONL.

### Phase 3 – Code & Additional Web
1. Download a heavily filtered subset of **The Stack v2** (target 1.5–2.5 TB after filtering).  
   Prefer high-quality languages and apply additional quality filters.
2. Add selected high-quality FineWeb dumps or the sample-350BT if you still have room.

### Phase 4 – Mixing & Local Training
1. Create shuffled mixtures on the remote storage.
2. Copy active training batches (up to ~4–5 TB) to local disk.
3. Keep a clean `DATA_ATTRIBUTION.md` and license manifest.

---

## Practical Tips

- Prefer **streaming + on-the-fly filtering** for FineWeb and The Stack instead of full downloads.
- Always write processed data as JSONL with consistent schema.
- Keep the SFT / instruction data relatively small and high-signal.
- Monitor disk usage closely. Leave at least 1 TB free on remote storage as buffer.
- Start training experiments as soon as Phase 1 + peS2o + FineWeb-Edu are ready. You do not need the full mixture before starting.

---

## Next Actions for the Agent

1. Set up the directory structure.
2. Begin Phase 1 downloads and conversions immediately.
3. Start FineWeb-Edu and peS2o downloads in parallel (they are high priority).
4. Maintain license fields and attribution files from day one.

This plan prioritizes quality over raw volume while staying realistic for your 11.2 TB + 5 TB setup.
