# Technology and model comparison

## Decision basis

The working hackathon implementation is the starting point. Selection criteria are local processing, Kazakh/Russian accuracy, maintainability for three students, reproducibility and the measured hardware budget. Alternatives below are engineering comparisons, not benchmark rankings. The existing stack is retained until a controlled experiment justifies a change [S35].

## Server platform

| Alternative | Fit and tradeoff | Decision |
| --- | --- | --- |
| FastAPI with Python | Existing typed API and direct Python pipeline integration; heavy work stays outside the API | Retain [S22, S35] |
| Django with DRF | Suitable if a broader account/admin product becomes necessary; migration adds work | Reserve for changed requirements |
| NestJS with TypeScript | Shares language with UI; still requires Python model integration | No demonstrated benefit over existing API |

## Data storage

| Alternative | Fit and tradeoff | Decision |
| --- | --- | --- |
| SQLite and local files | Embedded deployment, transactions and no database server; current single-worker boundary | Retain [S32, S35] |
| PostgreSQL and object storage | Better candidate for a networked multiuser deployment; introduces services and access design | Future scaling option [S24] |
| JSON files and local files | Simple for a disposable demo; application must implement safe concurrent updates and recovery | Reject for mutable queue/review state |

SQLite is used with short transactions and WAL mode. The application uses a single worker and local files. This is a deliberate deployment boundary rather than a claim that SQLite meets arbitrary concurrent-server requirements.

## Component interaction and jobs

| Alternative | Fit and tradeoff | Decision |
| --- | --- | --- |
| REST, UI polling and separate SQLite-backed worker | Existing persisted jobs and real stages; one machine, one worker | Retain |
| Celery with Redis and REST | Suitable for multiple workers but adds broker, deployment and recovery concerns | Reconsider only for scaling [S23] |
| In-process background task | Fewer processes but ties inference lifetime and resources to the web process | Reject for the core flow |

The worker claims jobs transactionally, models run outside database transactions, and interrupted jobs become visible failures. This design must be evaluated as implemented; it does not use an outbox, SSE or distributed queue.

## Speech recognition

| Alternative | Evidence and limitation | Decision |
| --- | --- | --- |
| Kazakh Russian mixed CTC checkpoint | Current bundled model; local evidence files exist; controlled bilingual quality is incomplete | Baseline [S34, S35] |
| Whisper large v3 turbo | Multilingual comparison path and recorded small-clip tests; same data/normalization needed | ASR challenger [S02, S20, S35] |
| Kazakh-tuned Whisper turbo | Repository pins a community variant; mixed/Russian robustness requires separate checking | Development challenger [S35] |

The repository includes small synthetic-clip comparisons and real-audio timing records. Do not generalise those results to all meetings. Compare models on identical whole-meeting splits and report WER/CER separately by language. Public corpus studies such as KSC2 guide data design, not a guarantee for the current checkpoint [S01].

## Speaker diarization

| Alternative | Fit and limitation | Decision |
| --- | --- | --- |
| sherpa onnx segmentation plus speaker embeddings | Current local pipeline with pinned assets | Retain and measure DER [S33, S35] |
| pyannote pipeline | Established alternative; exact model access, dependencies and license must be checked | Controlled comparison if feasible [S04] |
| Manual speaker assignment only | Low compute, high manual effort and no automatic grouping | Human baseline and correction fallback |

Speaker clusters are not verified identities. Manual mapping to named participants remains necessary.

## Language models for minutes

The exact candidates are Qwen3-4B-Instruct-2507, Llama-3.1-8B-Instruct, Gemma-3-12B-IT and NVIDIA-Nemotron-3-Nano-30B-A3B-BF16. The latter three are comparison candidates, not installed replacements. Card context limits describe model capabilities, not the configured Hattama runtime.

| Model | Model scale and context | Language and resource consideration | Project decision |
| --- | --- | --- | --- |
| Qwen3 4B Instruct 2507 | 4B dense; upstream context 262144 tokens | Existing 4-bit local checkpoint; Windows application limits total context to 2048 and output to 512 tokens | Retain baseline; improve measured errors [S21, S35] |
| Llama 3.1 8B Instruct | 8B dense; 128K context | Its eight explicitly supported languages exclude Kazakh/Russian; custom Llama license and adaptation need review | Conditional research candidate, not a bilingual default [S29] |
| Gemma 3 12B IT | 12B class; 128K input context | Card describes 140+ languages; this is not a Kazakh minutes benchmark. Larger memory footprint; Gemma terms apply | Larger multilingual challenger if resources permit [S30] |
| Nemotron 3 Nano 30B A3B | Hybrid MoE; about 30B total and 3B active; up to 1M context | Listed supported languages do not establish Kazakh/Russian coverage; low active count does not remove total-weight storage cost | Resource-gated challenger; NVIDIA model license [S31] |

A rough arithmetic check gives about 2, 4, 6 and 15 GB for weights alone at 4 bits per parameter for the nominal sizes above. These are estimates, not measured RAM/VRAM requirements; scales, embeddings, caches, activations and runtime overhead add memory. MoE still stores inactive experts. Neither Gemma 12B nor Nemotron 30B is promised to fit the recorded 4 GB GPU. Quantization or offloading changes the performance comparison and must be disclosed.

Run generation on the same corrected transcript set first to isolate generation quality. Compare source-supported task precision, task recall, owner/date correctness, summary errors, schema failures, processing time and memory. Use the same output schema and documented decoding settings; allow model-appropriate templates. Then measure the full ASR-to-DOCX pipeline. Qwen is retained for integration and resource evidence, not because an unperformed benchmark proved it best.

## Live meeting development

| Alternative | Dependency and limitation | Decision |
| --- | --- | --- |
| Zoom RTMS | Authorised app, media scopes, events and credits; new adapter and streaming evaluation | First external-connector candidate, not implemented [S26] |
| Google Meet Media API | Current documented preview access restrictions | Defer and recheck availability [S27] |
| Local microphone capture | Suitable for an in-room meeting; does not guarantee remote participant audio | Separate possible local extension |

The shipped baseline ingests uploaded recordings and keeps inference local. Adding a meeting-provider connection does not imply sending meeting content to a cloud AI service. A live feature requires a separately reviewed scope, permission model, buffer/reconnect behavior and latency measurements. The old 15-second live target is not a current performance claim.
