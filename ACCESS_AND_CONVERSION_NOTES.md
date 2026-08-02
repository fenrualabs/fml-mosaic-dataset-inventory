# Access and Conversion Notes for FML-Mosaic Datasets

Practical guidance for loading, streaming, and converting the large-scale datasets in the inventory into formats compatible with your existing ~26GB JSON holdings (e.g., JSONL, Parquet).

## General Best Practices (Hugging Face Datasets Library)

```python
from datasets import load_dataset

# Streaming (recommended for TB-scale — no full download)
ds = load_dataset("HuggingFaceFW/fineweb", name="sample-100BT", split="train", streaming=True)

for example in ds:
    # process example["text"] etc.
    pass

# With shuffle buffer for better mixing while streaming
ds = ds.shuffle(seed=42, buffer_size=10000)

# Local download of subset or full (use with care for large ones)
# huggingface-cli download --repo-type dataset HuggingFaceFW/fineweb --local-dir ./fineweb --include "sample-10BT/*"
```

- Prefer **streaming=True** for FineWeb, RedPajama-V2, Dolma, The Stack, Common Pile large parts, CulturaX, etc.
- Most modern datasets are already in Parquet (efficient). The HF Datasets server auto-converts many to Parquet.
- Use `datatrove` (HuggingFace) for FineWeb-style processing pipelines.
- For very large: snapshot_download with allow_patterns or huggingface-cli with --include filters.
- Convert to JSONL:
  ```python
  # After loading or iterating
  with open("output.jsonl", "w") as f:
      for ex in ds:
          f.write(json.dumps({"text": ex["text"], ...}) + "\n")
  ```
- Or keep as Parquet and use Polars / DuckDB / Spark for filtering/mixing with your JSONs.

## Specific Notes

**FineWeb / FineWeb-2 / FineWeb-Edu**  
- Streaming highly recommended. Use specific dump configs or samples (10BT/100BT/350BT).  
- datatrove ParquetReader works well.

**The Stack v2**  
- May require accepting terms / contact for full bulk. Subsets easier.  
- Provenance via SWHIDs — useful for filtering.

**Common Pile components**  
- Individual datasets are smaller and easier to load fully.  
- See COMMON_PILE_COMPONENTS.md for links. Many are already clean text.

**Dolma / peS2o / OpenWebMath**  
- Standard load_dataset works; some require trust_remote_code=True or custom scripts.

**OpenMathInstruct / Nemotron Post-Training**  
- Smaller (GB scale), easy full download. CC-BY-4.0 or NVIDIA commercial-friendly.  
- Nemotron-Post-Training-Dataset-v1/v2 and collections under nvidia/ for math, code, STEM, tool use, etc.

**SFT datasets (UltraChat, OpenOrca, OASST, Tulu, Magpie)**  
- Small enough for full load. Easy to convert to chat/JSON formats.

## Mixing with Existing 26GB JSONs
1. Stream or download selected high-priority sources.  
2. Apply your quality filters / dedup.  
3. Convert to consistent schema (e.g. {"text": ..., "source": ..., "license": ...}).  
4. Concatenate / interleave with existing data.  
5. Re-deduplicate at the end if needed (MinHash or exact).

## Tools
- `datasets` library + streaming  
- `huggingface_hub` / huggingface-cli  
- `datatrove`  
- Polars / Pandas / DuckDB for local processing  
- Apache Arrow / Parquet for intermediate storage

Always re-check live HF dataset cards for any access gates, latest license text, or required agreements before bulk use.

Continued expansion of the inventory ongoing.
