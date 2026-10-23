# Verification and evaluation plan

## Research questions and baselines

RQ1 asks how accurately candidate ASR models transcribe Kazakh, Russian and mixed meeting speech. Compare the current mixed-CTC model and the pinned Whisper turbo alternatives on exactly the same test recordings, then select an implementation candidate using quality and resource results [S01–S04, S20]. RQ2 asks whether source-linked neural minutes retain decisions and task tuples better than a deterministic extractive template. RQ3 asks whether the complete review workflow reduces active preparation time without reducing factual quality.

For the extractive baseline, freeze a bilingual cue list on development data, select complete segments containing agreed decision/action cues, retain the original text and evidence ID, and leave owner/date null unless explicitly annotated by the rule. This deliberately simple baseline measures the value and cost of neural abstraction. Do not change its cues after looking at the test set.

## Data and experimental separation

Target a pilot collection of 30 consented meetings of 10–30 minutes: ten primarily Kazakh, ten primarily Russian and ten mixed. Allocate six to development, six to validation and eighteen to frozen testing, balanced as two/two/six within each stratum. This is a small feasibility sample, not a population estimate. If the target cannot be reached, report actual counts and narrow the claims.

Keep every recording, derivative chunk and duplicate in the same split. Prefer disjoint recurring teams and speakers across splits; if that is infeasible, document the overlap and resulting limitation. Do not split segments from one meeting between tuning and testing. Public corpora may support development but must not enter the test set if they have influenced prompts, model selection or tuning. Pretrained-model exposure to public data cannot be fully excluded, so the principal test should be newly recorded consented meetings.

Two bilingual annotators independently transcribe and annotate test decisions/actions. Adjudicate disagreements without seeing system identity. Record language spans, timestamps, speaker turns, important decisions and task tuples (action, owner or null, deadline or null, evidence). Define rules for suggestions versus accepted decisions, withdrawn commitments, ambiguous owners and relative dates before annotation. Report agreement before adjudication and use the adjudicated set as the reference. The repository contains hackathon recordings and small synthetic/real-audio checks. A consented, independently annotated diploma test set with frozen splits has not been supplied.

## Measurement definitions

| Measure | Definition and reporting rule |
| --- | --- |
| WER and CER | Levenshtein edits divided by reference words/characters; corpus totals plus per-meeting values. Unicode NFC, casefolding and punctuation normalization are fixed; preserve Kazakh letters. Report empty-reference insertions separately. |
| Mixed speech | Report whole-meeting WER and manually aligned language-span error; never assign languages only from the system hypothesis. |
| Supported-item precision | Supported generated decisions/actions divided by all generated decisions/actions; check recording and source transcript. Empty output is not scored as perfect. |
| Decision recall | Correctly retained reference decisions divided by annotated reference decisions; report omissions separately. |
| Task-tuple F1 | One-to-one matching of semantically equivalent actions with correct owner and deadline, including null; report precision, recall and F1 by stratum. |
| Unsupported owner/date rate | Incorrect filled owner/date fields divided by filled fields; separately report missing required fields. |
| DER | Missed speech, false alarm and speaker confusion divided by reference speaker time; 0.25-second collar and overlap included. |
| Real-time factor | Processing wall time divided by recording duration; report queue, upload and cold model load separately. |
| Human effort | Active minutes to create an accepted protocol, correction count, task completion and reviewer factual-quality score. |

The repository includes ai/evaluate.py, ai/metrics.py and recorded evidence. Their exact metrics and input provenance must be checked for each experiment. Semantic support, task matching and DER require annotated data and the planned evaluation process. Unit tests of this utility are not model-quality results.

## Conditions and targets

Provisional quality gates are WER at most 25% Kazakh, 20% Russian and 30% mixed; supported-item precision at least 95%; task-tuple F1 at least 0.80 per stratum; and no automatic approval. These thresholds are planning targets pending a pilot and supervisor review. Report decision recall alongside precision so an empty or overly conservative summary cannot appear successful. A high-risk false owner/deadline assignment requires review even if aggregate metrics pass.

Use a declared reference machine with a proposed single GPU of at least 16 GB VRAM, 32 GB system RAM and SSD, but confirm actual model memory fit before committing to these specifications. Run ASR and generation sequentially if needed. Record GPU/CPU model, memory, operating system, library versions, model hashes, quantization, decoding and prompt. Test 1-, 10- and 30-minute inputs where feasible, one active job, warm and cold runs separately, three runs per performance fixture, and report all failures. If no suitable GPU is available, use a smaller candidate and revise the latency target transparently. Report RTF; set a feasible acceptance target after the pilot. The recorded full-pipeline run is slower than real time, so RTF at most 1.0 is not a supported baseline promise.

For metadata APIs, run a five-minute warm-up followed by ten minutes at five local clients and a declared fixture meeting set; report p50/p95 and error rates. Inject worker termination, repeated job claims, database lock contention, invalid JSON, silent audio, wrong-language output, cross-meeting evidence IDs and concurrent review saves. Verify the state and access invariants, not merely HTTP success codes.

## Usability study

Recruit 6–8 representative bilingual users, separate from annotators where possible. Each prepares minutes for two matched recordings: one with a manual audio player and text editor, one with the platform. Counterbalance order and recording assignment; do not give the same recording twice to one user. Keep the required minutes template and accuracy criteria identical. Measure active time separately from waiting time, independent task completion, correction effort and blinded reviewer quality.

Targets are at least 80% independent task completion and at least 20% lower median active preparation time without lower factual quality. With this small sample, report individual paired results and medians; bootstrap uncertainty by meeting or participant when appropriate. Do not claim statistical or population-level superiority from a small convenience sample.

## Error analysis and release decision

Run generation both on ASR transcripts and on corrected reference transcripts to isolate error propagation. Compare no-evidence prompting with source-constrained prompting only on development/validation data before freezing the selected variant. Review failures by language, overlap, noise, proper names, omissions, unsupported statements and attribution [S05–S10]. Store raw result records and a reproducible experiment manifest; label unfinished experiments as not run.

A release requires passing mandatory functional tests, documented unresolved limitations and supervisor agreement on any unmet target. No benchmark table in this package contains invented measurements. The full diploma benchmark has not been run.

## Live-mode evaluation

This evaluation applies only if the planned live extension is implemented. Replay the same consented recordings through a controlled authorised meeting and compare the finalized live result with upload mode. Record chunk duration, overlap handling, event duplication, disconnect/reconnect, missing audio and late decision corrections. Measure p95 chunk-close-to-visible-text latency against a hardware-specific target agreed before testing; report provider and network delays separately. Verify that provisional minutes cannot be approved, that missing media is disclosed, and that final reconciliation removes duplicate text without erasing corrections. Use one active session for the first benchmark and state this capacity limit explicitly.

## Model comparison experiment

Retain Qwen3-4B as the integrated baseline. Compare an extractive template and, subject to memory/language feasibility, Gemma 3 12B, Llama 3.1 8B and Nemotron 3 Nano 30B A3B. Use the same corrected transcripts and required output schema, record each exact checkpoint/template and compare factuality, recall, latency and memory. A candidate that cannot run within the declared budget is reported as infeasible rather than assigned an invented score. No head-to-head results for these three alternatives are supplied.

## Preliminary evidence from the repository

| Record | Observed result | Interpretation and limit |
| --- | --- | --- |
| Windows original-model run | 20.7949 s synthetic Russian audio; 196.97 s full pipeline; 6 segments, 2 speakers and 2 tasks | Recorded end-to-end evidence; RTF about 9.47; omitted deadline and incorrect summary noted |
| Real 45-second excerpt | 62.371 s pipeline; 6 segments, 2 speaker tracks, 0 tasks | Timing/count evidence only; no supplied reference supports a task recall score |
| Synthetic mixed 5.879-second clip | WER 0.30 mixed-CTC; 0.50 base-turbo; 0.30 Kazakh-turbo on ten reference words | Small synthetic comparison; not representative bilingual meeting accuracy |

These values are read from committed ai/evidence files at baseline 13d2271 [S35], not newly measured in this documentation update. The Windows evidence file reports an older 240-check collection including a legacy prototype; the current README reports 171 after layout consolidation. Counts refer to different scopes and must not be combined. Fresh validation results and limitations are recorded separately in submission/verification.md.
