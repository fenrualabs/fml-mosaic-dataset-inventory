# FML-Mosaic-527B Dataset Inventory (Expanded)

**Compiled for Fenrua Labs / FML-Mosaic-527B text generation model training.**  
**Date:** 2026-08-02 (updated with continued deep search)  
**Focus:** High-quality text-only datasets. Prioritize permissive licenses (Apache-2.0, MIT, BSD, ODC-By, CC-BY, Public Domain, commercially permissive). Avoid or flag restrictive (NC, unclear).  
**Sources searched:** Hugging Face, GitHub, Common Crawl derivatives, AllenAI, BigCode, NVIDIA, EleutherAI, Papers with Code, Kaggle, academic repos. Extensive multi-round deep search.  

**User already has ~26GB JSONs.** This extends resources.  

**Last Overkill Prompt (as requested):**  
"You are a dataset acquisition specialist. Your mission is to find every possible high-quality text dataset for training a large-scale text generation model, covering code, math, STEM, general web text, books, academic papers, and conversational data. Use the connected GitHub search tool with precise queries, not vague ones. Also, search Hugging Face datasets, Kaggle, Common Crawl derivatives, academic repositories like Allen Institute and Papers with Code, and any other credible source. For each dataset, document its name, URL, estimated size, license, language coverage, content type, quality notes, and access method. Prioritize permissively licensed data like Apache two point zero, MIT, BSD, or CC-BY. Explicitly avoid anything with restrictive terms or unclear licensing. Organize everything into a clean, structured markdown report with sections by category and a summary table. Include direct links and note any conversion steps needed. Be exhaustive, not selective. Leave no stone unturned."

---

## 1. General / Web Text / Pretraining Corpora

### Common Pile v0.1
- **URL:** https://huggingface.co/common-pile | Collections: https://huggingface.co/collections/common-pile/common-pile-v01-raw-data | Paper: https://arxiv.org/abs/2506.05209 | GitHub: https://github.com/r-three/common-pile/
- **Size:** 8 TB raw; ~1.8 TB filtered/deduped. ~233M documents.
- **License:** Public Domain + Openly Licensed sources (highly permissive / license-safe).
- **Languages:** Multilingual, English dominant.
- **Content:** 30 sources: research papers, code, books, encyclopedias, educational materials, audio transcripts, etc. Includes arxiv_papers, arxiv_abstracts, caselaw, biodiversity, etc.
- **Quality Notes:** Largest fully open/permissive pretraining set. Used to train competitive Comma 7B models. Excellent for commercial use.
- **Access:** HF collections (raw + filtered). Streaming recommended.

### FineWeb (HuggingFaceFW/fineweb)
- **URL:** https://huggingface.co/datasets/HuggingFaceFW/fineweb
- **Size:** ~15-18.5T tokens (~54 TB disk).
- **License:** ODC-By 1.0 (+ Common Crawl ToU).
- **Languages:** English.
- **Content:** Heavily filtered, deduplicated Common Crawl (96 dumps). High quality web text.
- **Quality Notes:** Outperforms C4, Dolma, Pile, SlimPajama, RedPajama on many benchmarks. Includes FineWeb-Edu subset (educational filter, 1.3T+).
- **Access:** HF load_dataset / streaming. Subsets available (10BT, 100BT, etc.).

### FineWeb-2
- **URL:** https://huggingface.co/datasets/HuggingFaceFW/fineweb-2 | GitHub: https://github.com/huggingface/fineweb-2
- **Size:** Large (billions of rows, multi-lingual scale).
- **License:** ODC-By.
- **Notes:** Multilingual extension / improved pipeline.

### RefinedWeb (tiiuae/falcon-refinedweb)
- **URL:** https://huggingface.co/datasets/tiiuae/falcon-refinedweb
- **Size:** Public extract ~500-650B tokens / ~2.8 TB clean text (968M pages); full was ~5T.
- **License:** ODC-By 1.0 (+ CC ToU).
- **Languages:** English.
- **Content:** Stringent filtering + large-scale deduplication of Common Crawl. Used for Falcon models.
- **Quality Notes:** High quality web-only. Good complement to FineWeb.
- **Access:** HF.

### Dolma (allenai/dolma)
- **URL:** https://huggingface.co/datasets/allenai/dolma | https://allenai.github.io/dolma/
- **Size:** 3 trillion tokens (earlier versions; check latest Dolma 3 for updates ~5.9T mixes).
- **License:** ODC-BY (updated from ImpACT).
- **Languages:** English primarily.
- **Content:** Diverse mix of web, academic publications, code, books, encyclopedic.
- **Quality Notes:** Open, well-documented from AllenAI/OLMo project.
- **Access:** HF.

### RedPajama-Data / V2 (togethercomputer)
- **URL:** https://huggingface.co/datasets/togethercomputer/RedPajama-Data-V2 (and V1)
- **Size:** V2 ~30T tokens (deduped); V1 ~1.2T.
- **License:** Apache-2.0 (code); data subject to source licenses + CC ToU. Quality signals provided.
- **Languages:** Multi (EN dominant).
- **Content:** CommonCrawl, C4, GitHub, Books, ArXiv, Wikipedia, StackExchange.
- **Notes:** Good annotations for further filtering. Books subset may have issues (often dropped).

### SlimPajama-627B
- Apache 2.0, 627B tokens cleaned/deduped RedPajama.

### The Pile (EleutherAI/pile)
- **URL:** https://huggingface.co/datasets/EleutherAI/pile | https://pile.eleuther.ai/
- **Size:** ~825 GB / 22 components.
- **License:** Mixed (repo MIT; individual components vary — check carefully). Successor is Common Pile.
- **Notes:** Classic but mixed licenses; prefer Common Pile for safety.

### C4 (allenai/c4)
- **URL:** https://huggingface.co/datasets/allenai/c4
- **Size:** Large (hundreds of GB).
- **License:** ODC-By or similar (from Common Crawl).
- **Notes:** Colossal Cleaned Common Crawl. Foundational but older quality filtering.

---

## 2. Code Datasets

### The Stack v2 (bigcode/the-stack-v2)
- **URL:** https://huggingface.co/datasets/bigcode/the-stack-v2 | Project: https://www.bigcode-project.org/
- **Size:** Full ~67.5 TB uncompressed; deduped ~32 TB; train sets hundreds of billions tokens. 658+ languages.
- **License:** Filtered to permissive licenses only (list of ~193 including MIT, Apache, BSD, etc.). "other" on HF but provenance for each file. Requires contact agreement for full access sometimes.
- **Content:** Source code from Software Heritage, issues, notebooks, commits.
- **Quality Notes:** Gold standard for code LLMs. Used for StarCoder2. SWHIDs for transparency.
- **Access:** HF (agree to terms), subsets available. Paper: arXiv:2402.19173.

### The Stack v1 / StarCoderData (bigcode/the-stack, bigcode/starcoderdata)
- **URL:** https://huggingface.co/datasets/bigcode/the-stack | https://huggingface.co/datasets/bigcode/starcoderdata
- **Size:** Stack ~6.4 TB (v1.1 near-dedup); StarCoderData 783 GB code + issues + notebooks.
- **License:** Permissive filtered (Apache-compatible etc.).
- **Notes:** Earlier version; still excellent. 86-358 languages depending on version.

---

## 3. Math / STEM

### OpenWebMath (open-web-math/open-web-math)
- **URL:** https://huggingface.co/datasets/open-web-math/open-web-math | GitHub: https://github.com/keirp/OpenWebMath
- **Size:** 14.7B tokens / ~6.3M docs / ~27-56 GB.
- **License:** ODC-By 1.0 (+ CC ToU).
- **Languages:** English.
- **Content:** High-quality mathematical web text from Common Crawl (LaTeX extracted, filtered).
- **Quality Notes:** Models trained on it punch above weight for math. Paper: arXiv:2310.06786.
- **Access:** HF load_dataset.

### OpenMathInstruct-1 (nvidia/OpenMathInstruct-1)
- **URL:** https://huggingface.co/datasets/nvidia/OpenMathInstruct-1
- **Size:** 1.8M problem-solution pairs / ~8.94 GB.
- **License:** NVIDIA License (permits commercial usage).
- **Content:** Synthesized code-interpreter solutions for GSM8K + MATH using Mixtral.
- **Quality Notes:** Commercially permissive. Strong for math instruction tuning. Paper arXiv:2402.10176.

### OpenMathInstruct-2 (nvidia/OpenMathInstruct-2)
- **URL:** https://huggingface.co/datasets/nvidia/OpenMathInstruct-2
- **Size:** 14M problem-solution pairs / ~12.6 GB.
- **License:** CC-BY-4.0.
- **Content:** Larger scale, using Llama-3.1-405B, including new synthesized questions. Decontaminated.
- **Quality Notes:** Excellent scale-up for math SFT. Paper arXiv:2410.01560.

### Proof-Pile (hoskinson-center/proof-pile)
- **URL:** https://huggingface.co/datasets/hoskinson-center/proof-pile
- **Size:** 13 GB / 8.3B tokens.
- **License:** Apache-2.0.
- **Content:** Mathematical text: informal + formal math from arXiv, libraries, Wikipedia, StackExchange, etc.
- **Quality Notes:** Used in Llemma / Proof-Pile-2 (larger ~55B tokens combining OpenWebMath + AlgebraicStack + arXiv).

### MathPile (GAIR-NLP/MathPile)
- **Size:** ~9.5B tokens.
- **License:** CC BY-NC-SA 4.0 (**non-commercial** — flag / avoid for commercial).

### Other STEM: arXiv extracts (in Common Pile, Dolma, RedPajama), AlgebraicStack (code for math).

---

## 4. Books

### Project Gutenberg (manu/project_gutenberg + raw)
- **URL:** https://huggingface.co/datasets/manu/project_gutenberg | https://www.gutenberg.org/ | Scripts: various including pgcorpus/gutenberg, google-deepmind/pg19
- **Size:** ~75k books / 14.4 GB on HF; full downloads ~50GB+.
- **License:** Public Domain (US) for vast majority. Project Gutenberg License.
- **Languages:** Mostly English + others.
- **Content:** Classic literature, poetry, etc. Header/footer marked.
- **Quality Notes:** Clean long-form text. PG-19 subset: 28k pre-1919 books for long-context.
- **Access:** HF or direct download + scripts. Avoid Books3 / LibGen (copyright issues).

### Common Pile books components: Included in the 8TB (LOC, Internet Archive digitized PD volumes).

---

## 5. Academic / Papers

### arXiv components in Common Pile
- **URL:** https://huggingface.co/datasets/common-pile/arxiv_papers | arxiv_abstracts
- **Size:** Hundreds of thousands of papers / abstracts.
- **License:** Openly licensed / as per arXiv (many CC).
- **Notes:** Full papers mixed; abstracts safer. Use olmocr (allenai/olmocr) for PDF linearization if needed.

### Other: PubMed, etc. in Dolma / Common Pile / RedPajama.

---

## 6. Conversational / Instruction / Alignment / SFT

### UltraChat 200k (HuggingFaceH4/ultrachat_200k)
- **URL:** https://huggingface.co/datasets/HuggingFaceH4/ultrachat_200k
- **Size:** 1.62 GB / ~515k examples (SFT/Gen splits).
- **License:** MIT.
- **Languages:** English.
- **Content:** Filtered multi-turn ChatGPT dialogues. High quality for SFT.
- **Quality Notes:** Used for Zephyr. Original UltraChat larger but check upstream (some NC notes).
- **Access:** HF load_dataset.

### OpenAssistant OASST1 (OpenAssistant/oasst1)
- **URL:** https://huggingface.co/datasets/OpenAssistant/oasst1
- **Size:** 161k messages / 66k trees.
- **License:** Apache-2.0.
- **Languages:** 35 languages (EN, ES dominant).
- **Content:** Human-generated + annotated conversation trees with quality/toxicity labels.
- **Quality Notes:** Excellent for alignment. Ready-for-export subset.
- **Access:** HF.

### OpenOrca (Open-Orca/OpenOrca)
- **URL:** https://huggingface.co/datasets/Open-Orca/OpenOrca
- **Size:** ~2.9M examples (1M GPT-4 + 3.2M GPT-3.5 completions on FLAN).
- **License:** MIT.
- **Languages:** English.
- **Content:** Augmented FLAN for reasoning / instruction following.
- **Quality Notes:** High quality for Orca-style training. Streaming recommended.
- **Access:** HF.

### Tulu-3 SFT Mixture (allenai/tulu-3-sft-mixture)
- **URL:** https://huggingface.co/datasets/allenai/tulu-3-sft-mixture | Collection: https://huggingface.co/collections/allenai/tulu-3-datasets
- **Size:** 100K-1M scale mixture.
- **License:** ODC-BY-1.0 (note: some subsets may have different/non-commercial; research artifact).
- **Content:** Curated mixture for Tulu-3 post-training, targeting core skills, diversity, clear provenance.
- **Quality Notes:** Modern open post-training data. Check individual subsets carefully.

### Magpie (Magpie-Align)
- **URL:** GitHub https://github.com/magpie-align/magpie | HF Magpie-Align collections
- **Size:** Millions (e.g. 1M from Llama-3.1).
- **License:** Method MIT; generated data often inherits from base model (Llama community or CC-BY-NC in some cases). Check specific releases (Llama-3.1 versions more friendly).
- **Content:** Self-synthesized alignment data by prompting aligned LLMs with pre-query templates. High quality synthetic.
- **Notes:** Useful for generating more data yourself with permissive base models.

### ShareGPT variants: Various (e.g. unfiltered, 52k/90k). Licensing murkier (scraped conversations). Prefer above.

---

## 7. Other / Kaggle / Smaller / Tools

- Kaggle has many smaller text datasets (e.g. large-scale English text), but not competitive with above for scale. Search Kaggle for specific domains.
- Synthetic generators: Magpie method, tools for creating from text/PDFs.
- AllenAI olmocr: Toolkit for turning PDFs into LLM-ready text.
- Wikipedia dumps, StackExchange dumps (often in the large corpora above).

---

## Summary Table (Selected Priority - Updated)

| Category       | Dataset                  | Approx Size          | License                  | Priority |
|----------------|--------------------------|----------------------|--------------------------|----------|
| General        | Common Pile v0.1        | 8 TB                | PD/Open                  | Highest |
| General        | FineWeb                 | 15T+ tokens         | ODC-By                   | High    |
| General        | RefinedWeb (extract)    | 500-650B tokens     | ODC-By                   | High    |
| Code           | The Stack v2            | 30-67 TB            | Permissive filt.         | Highest |
| Math           | OpenWebMath             | 14.7B tokens        | ODC-By                   | High    |
| Math           | OpenMathInstruct-2      | 14M pairs           | CC-BY-4.0                | High    |
| Math           | OpenMathInstruct-1      | 1.8M pairs          | NVIDIA (commercial OK)   | High    |
| Math           | Proof-Pile              | 8.3B tokens         | Apache-2.0               | Medium  |
| Books          | Project Gutenberg       | 14+ GB / 75k        | Public Domain            | High    |
| Conversational | UltraChat 200k          | 1.6 GB              | MIT                      | High    |
| Conversational | OASST1                  | 161k msgs           | Apache-2.0               | High    |
| Conversational | OpenOrca                | 2.9M                | MIT                      | High    |
| SFT            | Tulu-3 mixture          | ~100k-1M            | ODC-BY (check subsets)   | High    |
| General        | Dolma                   | 3T tokens           | ODC-BY                   | High    |

**Recommendations for FML-Mosaic-527B (updated):**  
1. **License-safe core pretraining**: Common Pile v0.1 + FineWeb + RefinedWeb extract + The Stack v2.  
2. **Math/STEM boost**: OpenWebMath + OpenMathInstruct-1/2 + Proof-Pile.  
3. **Books/long-context**: Project Gutenberg / Common Pile books.  
4. **Post-training / SFT**: UltraChat 200k + OASST1 + OpenOrca + Tulu-3 mixture (vet subsets) + Magpie-generated if using permissive bases.  
5. Always re-check the live HF dataset cards for the absolute latest size/license notes and use streaming where possible. Deduplicate and mix carefully against your existing ~26 GB JSON holdings.  
6. Agent can filter/add to your data.

**This inventory will continue to be updated.** Report issues or additional finds in this repo.

**Repo:** https://github.com/fenrualabs/fml-mosaic-dataset-inventory
