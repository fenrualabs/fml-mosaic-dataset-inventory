# FML-Mosaic-527B Dataset Inventory and Operating Plan

This repository is the operational source of truth for building the
FML-Mosaic-527B training corpus. Its inventory files define the permitted
public sources and their order. This README defines the storage, conversion,
and training workflow so later operators and agents do not infer a different
process from stale receipts or legacy controls.

## Goal

Preserve the existing WOLFRIG corpus (about 25 GB, 1,501 original resources),
then extend it with the datasets in [AGENT_START_PLAN.md](AGENT_START_PLAN.md)
to a high-quality practical corpus below the 11.2 TB Hugging Face storage
limit. Keep at least 1 TB remote free: the remote corpus ceiling is therefore
**10.2 TB**.

Current language scope is **English only**. Ingest only English source splits
or English-source components, and defer any other language until the plan is
explicitly changed.

The existing corpus is part of the final program. It must not be deleted,
moved, overwritten, or silently re-cleaned.

## Authoritative locations

| Role | Location | Rule |
|---|---|---|
| Immutable existing corpus | WOLFRIG: `/mnt/f/Fenrua-Corpus/30-training-ready/canonical-jsonl-20260802-001/` | Read-only source of the existing generation. |
| Existing source companions | WOLFRIG: `/mnt/f/Fenrua-Corpus/manifests/transformations/canonical-jsonl-20260802-001/` | Hashes, source bindings, and resource records stay outside training JSONL. |
| Local build/cache root | `/mnt/f/FML-Mosaic-527B-Corpus-Prep/data/` | Bounded temporary conversion and training cache. |
| Canonical remote corpus | Hugging Face dataset `Fenrua-Labs/FML-Mosaic-527B-Corpus` | Private while building; this is the canonical remote store. |
| Legacy HF control handoff | `Fenrua-Labs/FML-Mosaic-527B-Corpus-Prep` | Stale controls only; it does not govern this plan or receive corpus payloads. |

Do not rely on a static local-free-space figure in this document. Check
`df` before every new source, keep the plan's 1 TB capacity buffer, and do
not attempt to retain the full corpus locally. Reserve 2.5–3.0 TB for active
training and limit conversion staging to the remainder. The Hugging Face
dataset repository, not the local disk, is the durable corpus store.

## Canonical data contract

Every **newly converted** record uses exactly this JSONL schema, with no
hashes, URLs, resource paths, identifiers, or additional metadata in the
training record:

```json
{"text":"the actual content","source":"openwebmath","license":"ODC-By-1.0 + CommonCrawl-ToU"}
```

The only allowed license values are:

- `ODC-By-1.0 + CommonCrawl-ToU`
- `Public Domain`
- `MIT`
- `Apache-2.0`
- `CC-BY-4.0`
- `NVIDIA`
- `PD / Open`

Write raw-source details, remote revisions, hashes, shard checksums, row
counts, recovery state, and validation reports into companion manifests.
Keep attribution in `DATA_ATTRIBUTION.md` and phase-specific manifests.

A source-derived `jsonl/phase*/` path is preserved conversion output, not
automatically training input. Only `jsonl/training-ready/` is consumable by
a training mixture. Promotion requires a separate immutable-input canonical
writer, a passed exact-schema/hash validation, and a passed clean-text audit
with zero matches for URLs/emails, legacy vendor-or-model references,
credential/secret patterns, and labelled provenance. Input hashes, dropped-row
counts, source resources, and every validation receipt remain external.

### Existing WOLFRIG corpus

The preserved WOLFRIG final inclusion roots are immutable text-only input,
with 5,166 shards and separate companion bindings. Superseded legacy roots
are excluded; do not modify any original text-only files. Before it enters a
three-field mixture, complete its final audit, then create a separate wrapper
generation and an external join/index:

`output path + SHA-256 → source manifest/resource + SHA-256 → approved normalized license`

Only wrap a shard when its license can be mapped to one of the allowed values
from its source evidence. Keep an ambiguity report external and do not invent
a license value. The final verifier and wrapper validation report are required
before blending the existing generation.

Current state: the separate wrapper
`wolfrig-canonical-jsonl-20260802-001-clean` has passed full local and remote
verification for all 5,166 final-inclusion shards. The immutable original
remains unchanged; use only the verified wrapper in any mixture.

## Remote layout

```text
FML-Mosaic-527B-Corpus/
  README.md
  DATA_ATTRIBUTION.md
  jsonl/
    existing/             # schema-wrapped WOLFRIG only after validation
    phase1/               # preserved source-derived candidates
    phase2/
    phase3/
    sft/
    training-ready/       # only zero-residue canonical rows may be trained
      phase1/
      phase2/
      phase3/
      sft/
  manifests/
    existing/
    phase1/
    phase2/
    phase3/
    sft/
    training-ready/       # external lineage, hashes, and drop counts
  mixtures/
  validation/
    training-ready/       # external canonical validation and content audits
```

Each source is streamed into 512 MiB JSONL shards. A shard is uploaded only
after it is closed, JSON-valid, and recorded in a companion manifest with its
SHA-256 and record count. Upload the source manifest and validation result with
the shards. Verify the remote revision and checksums before reclaiming
generated local staging. Never reclaim the immutable WOLFRIG source.

A canonical training-ready source receives a second, stricter remote chain:
upload only its zero-residue JSONL under `jsonl/training-ready/`, publish its
canonical manifest and audits under matching external companion paths, verify
every remote hash, persist exactly one canonical completion event, and read the
receipt and event back from the Hub. Do not train from a phase path merely
because its original source receipt passed.

## Source execution order

Do not add alternative datasets or reorder these phases without an explicit
plan update.

### Phase 1 — complete in order

1. `open-web-math/open-web-math` — `openwebmath` — `ODC-By-1.0 + CommonCrawl-ToU`
2. `nvidia/OpenMathInstruct-1` — `openmathinstruct-1` — `NVIDIA`
3. `nvidia/OpenMathInstruct-2` — `openmathinstruct-2` — `CC-BY-4.0`
4. `manu/project_gutenberg` — English split (`en`) only for now —
   `project-gutenberg-en` — `Public Domain`. Do not process or upload
   non-English splits without an explicit future plan update.
5. `HuggingFaceH4/ultrachat_200k` — `ultrachat-200k` — `MIT`
6. `OpenAssistant/oasst1` — `oasst1` — `Apache-2.0`
7. `Open-Orca/OpenOrca` — `openorca` — `MIT`

For conversational data, retain ordered conversational text only. Never emit
message IDs, tree IDs, prompt IDs, response IDs, model labels, source URLs,
quality scores, or other external metadata in training JSONL.

### Phase 2 — after Phase 1 is validated and uploaded

1. `allenai/peS2o` (V2 `s2orc`, then `s2ag`) — ODC-By attribution required.
2. `HuggingFaceFW/fineweb-edu` — begin `sample-10BT`, then `sample-100BT`,
   then `sample-350BT`; use streaming.
3. Common Pile filtered components, highest value first: arXiv, books,
   education, science, and StackExchange. See
   [COMMON_PILE_COMPONENTS.md](COMMON_PILE_COMPONENTS.md).

### Phase 3 — only after Phase 2 is well underway

1. `bigcode/the-stack-v2` — selected permitted languages or `train-smol`;
   never bulk-download the full corpus.
2. `HuggingFaceFW/fineweb` — use the official sample configurations first.

### Phase 4 — keep small

Only after Phases 1–3 are progressing: selected public NVIDIA Nemotron SFT
sets for math, science, instruction, and software engineering. Store in
`jsonl/sft/` with the same schema and separate manifests.

## Conversion and upload procedure

1. Authenticate with the supplied Hugging Face credential. Never print or
   commit the token.
2. Read the live dataset card and license before processing each source. Use
   only public, plan-listed sources; do not bypass a gate or accept a new
   agreement on behalf of anyone.
3. Stream sources over approximately 100 GB; do not bulk-download them.
4. Extract content only. Drop empty records and clear credential material.
   Keep required source and license fields; exclude external control metadata.
5. Write 512 MiB atomic JSONL shards and separate progress/checksum manifests.
6. Validate exact keys, JSON validity, non-empty fields, allowed license
   values, no partial outputs, and manifest-to-shard checksum agreement.
7. Upload verified shards and all companion artifacts to the canonical HF
   corpus repository. Verify the remote commit and object checksums.
8. Record the upload, attribution, byte total, and remaining remote capacity.
   Reclaim only verified generated local staging if local training space is
   needed.

For ODC-By + Common Crawl sources, retain the required attribution in every
record and in `DATA_ATTRIBUTION.md`; see
[LICENSE_HANDLING_ODC_BY.md](LICENSE_HANDLING_ODC_BY.md).

## 1 GB rotating training batches

Hugging Face is the main storage; local storage is a high-speed working set.
Train from rotating approximately 1 GB units, normally two consecutive 512
MiB validated JSONL shards:

1. Read the remote mixture manifest and choose the next weighted source/shard
   pair using a persisted seed and cursor.
2. Download that unit to a local `training-cache/current/` directory.
3. Verify each shard’s SHA-256 against the remote manifest before parsing.
4. Parse the `text` field, tokenize/pack sequences locally, and run the
   training micro-batches. `source` and `license` remain available for
   accounting and attribution; they are not model tokens unless a future
   training recipe explicitly says otherwise.
5. Persist the training checkpoint, optimizer state, source cursor, random
   seed, consumed shard hashes, and mixture revision before moving on.
6. Fetch the next approximately 1 GB unit while the current one is being
   parsed or trained. With the stated fast connection, network transfer should
   be comfortably under five seconds; allow local parsing and token packing to
   overlap it.
7. After a confirmed checkpoint and next-unit prefetch, remove only the local
   cache copy. The canonical HF shard and its manifest remain untouched.

This makes training restartable without downloading the full multi-terabyte
corpus, while preserving a 2.5–3.0 TB local area for temporary training
mixtures, checkpoints, and cache headroom.

## Anti-drift rules

- This GitHub plan takes precedence over stale control-repository instructions.
- Preserve the existing WOLFRIG corpus and its external companions exactly.
- Do not put hashes, URLs, resource locations, IDs, or hidden control metadata
  inside training records.
- Do not change the schema, source list, phase order, remote capacity cap, or
  1 GB rotating-batch process without an explicit update to this repository.
- Record every completed source, validation result, remote revision, and
  training cursor in durable manifests/logs.
- Treat “downloaded” as incomplete. A source is complete only after validation,
  attribution, remote upload, remote verification, and a persisted receipt.

## Reference files

- [AGENT_START_PLAN.md](AGENT_START_PLAN.md) — ordered operating plan
- [DATASET_INVENTORY.md](DATASET_INVENTORY.md) — permitted source inventory
- [COMMON_PILE_COMPONENTS.md](COMMON_PILE_COMPONENTS.md) — component order
- [LICENSE_HANDLING_ODC_BY.md](LICENSE_HANDLING_ODC_BY.md) — attribution rules
- [ACCESS_AND_CONVERSION_NOTES.md](ACCESS_AND_CONVERSION_NOTES.md) — streaming
  and conversion notes
