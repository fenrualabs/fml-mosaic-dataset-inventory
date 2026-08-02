# FML-Mosaic-527B Dataset Inventory (Cleaned – Commercial-Safe Focus)

**Compiled for Fenrua Labs / FML-Mosaic-527B text generation model training.**  
**Date:** 2026-08-02 (cleaned)  
**Focus:** High-quality text-only datasets with permissive / commercial-friendly licenses (Apache-2.0, MIT, BSD, ODC-By, CC-BY, Public Domain, NVIDIA commercial licenses). Restricted / non-commercial items have been removed.  
**Sources searched:** Hugging Face, GitHub, Common Crawl derivatives, AllenAI, BigCode, NVIDIA, EleutherAI, Pleias, academic repos. Extensive multi-round deep search.  

**User already has ~26GB JSONs.** This extends resources with license-safe options.  

---

## 1. General / Web Text / Pretraining Corpora

### Common Pile v0.1
- **URL:** https://huggingface.co/common-pile | Collections: https://huggingface.co/collections/common-pile/common-pile-v01-raw-data | Paper: https://arxiv.org/abs/2506.05209 | GitHub: https://github.com/r-three/common-pile/
- **Size:** 8 TB raw; ~1.8 TB filtered/deduped.
- **License:** Public Domain + Openly Licensed sources only (highly permissive / license-safe).
- **Languages:** Multilingual, English dominant.
- **Content:** 30 curated sources: research papers, code, books, encyclopedias, educational materials, legal, patents, etc.
- **Quality Notes:** Largest fully open/permissive pretraining set. Excellent for commercial use.
- **Access:** HF collections (raw + filtered). Streaming recommended. See COMMON_PILE_COMPONENTS.md for full source list.

### Common Corpus (PleIAs/common_corpus)
- **URL:** https://huggingface.co/datasets/PleIAs/common_corpus
- **Size:** ~2.27 trillion tokens.
- **License:** Truly open — only public domain / uncopyrighted or free/permissive licenses.
- **Content:** Six collections (Open Culture, Open Government, Open Science, Open Web, Open Code, Open Semantic). Books, newspapers, scientific, legal/government, code, etc.
- **Quality Notes:** One of the strongest fully open large-scale corpora.

### FineWeb (HuggingFaceFW/fineweb)
- **URL:** https://huggingface.co/datasets/HuggingFaceFW/fineweb
- **Size:** ~15–18.5T tokens (~54 TB disk).
- **License:** ODC-By 1.0 (+ Common Crawl ToU).
- **Languages:** English.
- **Content:** Heavily filtered, deduplicated Common Crawl. High quality web text. Includes FineWeb-Edu subset.
- **Access:** HF load_dataset / streaming. Subsets available (10BT, 100BT, 350BT).

### FineWeb-2
- **URL:** https://huggingface.co/datasets/HuggingFaceFW/fineweb-2
- **Size:** ~20 TB scale, multilingual (1000+ languages).
- **License:** ODC-By.
- **Notes:** Multilingual extension (pair with FineWeb for English).

### RefinedWeb (tiiuae/falcon-refinedweb)
- **URL:** https://huggingface.co/datasets/tiiuae/falcon-refinedweb
- **Size:** Public extract ~500–650B tokens.
- **License:** ODC-By 1.0 (+ CC ToU).
- **Notes:** High-quality filtered Common Crawl. Used for Falcon models.

### Dolma (allenai/dolma)
- **URL:** https://huggingface.co/datasets/allenai/dolma
- **Size:** Multi-trillion tokens.
- **License:** ODC-BY.
- **Content:** Diverse mix of web, academic, code, books, encyclopedic.

### RedPajama-Data-V2 / SlimPajama-627B
- **URL:** https://huggingface.co/datasets/togethercomputer/RedPajama-Data-V2 | https://huggingface.co/datasets/cerebras/SlimPajama-627B
- **Size:** RedPajama-V2 ~30T tokens; SlimPajama 627B tokens.
- **License:** Apache-2.0 (code) + source licenses / CC ToU; SlimPajama Apache 2.0.
- **Notes:** Quality signals available for further filtering.

### C4 (allenai/c4)
- **URL:** https://huggingface.co/datasets/allenai/c4
- **License:** ODC-By (+ CC ToU).
- **Notes:** Classic cleaned Common Crawl.

---

## 2. Code Datasets

### The Stack v2 (bigcode/the-stack-v2)
- **URL:** https://huggingface.co/datasets/bigcode/the-stack-v2
- **Size:** Full ~67.5 TB; deduped ~32 TB; hundreds of billions of tokens. 600+ languages.
- **License:** Filtered to permissive licenses only (MIT, Apache, BSD, etc.) with file-level provenance.
- **Content:** Source code from Software Heritage + extras (issues, notebooks, commits).
- **Quality Notes:** Gold standard for code generation models (StarCoder2).
- **Access:** HF (may require agreement for full bulk).

### The Stack v1 / StarCoderData
- Earlier permissive-filtered versions still useful.

---

## 3. Math / STEM

### OpenWebMath
- **URL:** https://huggingface.co/datasets/open-web-math/open-web-math
- **Size:** 14.7B tokens / ~6.3M docs.
- **License:** ODC-By 1.0 (+ CC ToU).
- **Notes:** High-quality mathematical web text with LaTeX.

### OpenMathInstruct-1 (nvidia/OpenMathInstruct-1)
- **URL:** https://huggingface.co/datasets/nvidia/OpenMathInstruct-1
- **Size:** 1.8M problem-solution pairs.
- **License:** NVIDIA License (permits commercial usage).

### OpenMathInstruct-2 (nvidia/OpenMathInstruct-2)
- **URL:** https://huggingface.co/datasets/nvidia/OpenMathInstruct-2
- **Size:** 14M pairs.
- **License:** CC-BY-4.0.

### Proof-Pile
- **URL:** https://huggingface.co/datasets/hoskinson-center/proof-pile
- **Size:** 13 GB / 8.3B tokens.
- **License:** Apache-2.0.

### peS2o (allenai/peS2o)
- **URL:** https://huggingface.co/datasets/allenai/peS2o
- **Size:** ~39–67M documents / ~40–47B tokens / 308 GB.
- **License:** ODC-By.
- **Notes:** Cleaned open-access scientific papers (CS, physics, biology, chemistry, etc.).

### NVIDIA Nemotron Math / Science SFT series
- Commercially friendly (CC-BY-4.0 / NVIDIA Open Data License) high-quality math and STEM post-training data.

---

## 4. Books

### Project Gutenberg
- **URL:** https://huggingface.co/datasets/manu/project_gutenberg + raw Gutenberg / PG-19
- **Size:** ~75k books / 14+ GB.
- **License:** Public Domain (US) for vast majority.
- **Notes:** Clean long-form text. Excellent for long-context.

### Common Pile / Common Corpus book components
- Pre-1929 books, Library of Congress, Open Culture collections, etc.

---

## 5. Academic / Papers

- arXiv components inside Common Pile (arxiv_papers, arxiv_abstracts)
- peS2o scientific papers
- PubMed and other open sources inside Common Pile / Dolma

---

## 6. Conversational / Instruction / SFT

### UltraChat 200k (HuggingFaceH4/ultrachat_200k)
- **URL:** https://huggingface.co/datasets/HuggingFaceH4/ultrachat_200k
- **Size:** ~515k examples.
- **License:** MIT.

### OpenAssistant OASST1
- **URL:** https://huggingface.co/datasets/OpenAssistant/oasst1
- **Size:** 161k messages / 66k trees.
- **License:** Apache-2.0.

### OpenOrca
- **URL:** https://huggingface.co/datasets/Open-Orca/OpenOrca
- **Size:** ~2.9M examples.
- **License:** MIT.

### NVIDIA Nemotron Post-Training / SFT series
- Math, SWE/software engineering, Science, Instruction-Following, Agentic, etc.
- Predominantly CC-BY-4.0 or NVIDIA Open Data License (commercial use supported).

### Tulu-3 SFT Mixture (core safe subsets)
- **URL:** https://huggingface.co/collections/allenai/tulu-3-datasets
- **License:** ODC-BY overall (use only clearly permissive subsets).

---

## 7. Access & Conversion
See `ACCESS_AND_CONVERSION_NOTES.md` for streaming, loading, and converting large datasets to JSONL/Parquet to merge with your existing data.

---

## Summary Table (Commercial-Safe Priority)

| Category       | Dataset                      | Approx Size          | License                        | Priority |
|----------------|------------------------------|----------------------|--------------------------------|----------|
| General        | Common Pile v0.1            | 8 TB                | PD / Open                      | Highest |
| General        | Common Corpus               | 2.27T tokens        | Truly Open                     | Highest |
| General        | FineWeb (+ Edu / FineWeb-2) | 15T+ / multilingual | ODC-By                         | High    |
| Code           | The Stack v2                | 30–67 TB            | Permissive filtered            | Highest |
| Math           | OpenWebMath                 | 14.7B tokens        | ODC-By                         | High    |
| Math           | OpenMathInstruct-1/2        | 1.8M / 14M pairs    | NVIDIA / CC-BY-4.0             | High    |
| Math           | Proof-Pile                  | 8.3B tokens         | Apache-2.0                     | Medium  |
| STEM           | peS2o                       | ~40B tokens         | ODC-By                         | High    |
| Books          | Project Gutenberg           | 14+ GB / 75k        | Public Domain                  | High    |
| Conversational | UltraChat 200k              | ~515k               | MIT                            | High    |
| Conversational | OASST1                      | 161k msgs           | Apache-2.0                     | High    |
| Conversational | OpenOrca                    | 2.9M                | MIT                            | High    |
| SFT            | Nemotron Post-Training series | Various           | CC-BY-4.0 / NVIDIA             | High    |

**Recommended stack for FML-Mosaic-527B:**  
1. **Core pretraining**: Common Pile + Common Corpus + FineWeb (+ Edu) + The Stack v2  
2. **STEM**: peS2o + OpenWebMath + OpenMathInstruct + Proof-Pile + Nemotron Math/Science  
3. **Code / SWE**: The Stack v2 + Nemotron-SFT-SWE  
4. **SFT**: UltraChat + OASST1 + OpenOrca + Nemotron Post-Training series  
5. **Books / long-context**: Project Gutenberg + Common Pile / Common Corpus book sources  

All remaining entries prioritize permissive or commercially friendly licensing. Always re-verify the live Hugging Face dataset card and any linked LICENSE before bulk use.

**Repo:** https://github.com/fenrualabs/fml-mosaic-dataset-inventory
