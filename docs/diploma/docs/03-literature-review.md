# Literature review

## Review method and boundaries

This focused design review uses eleven scientific publications published in 2021–2025 and official product and technology sources. Scientific records were checked on ACL Anthology, the ISCA archive and PMLR; product claims were checked against official help pages on 23 October 2026. Searches covered Kazakh ASR, long-form transcription, diarization, meeting summarization, evidence alignment and summary evaluation. The reference register contains 35 meaningfully used sources.

Inclusion required a clear connection to a pipeline component, evaluation method or design risk. Papers without a usable method or relevant limitation were excluded. This is a structured engineering review, not an exhaustive systematic review. No paper is evidence that the proposed platform already works on Kazakhstan meeting data. The core includes nine papers from 2022–2025. Two 2021 papers are retained for their meeting-benchmark and evaluation methods; they are outside the rolling five-year window.

## Speech recognition and speaker attribution

KSC2 provides a substantial Kazakh speech resource that includes varied domains and code-switching [S01]. It is relevant to ASR development but does not provide the proposed meeting-minute annotations. Training or tuning on public speech cannot replace a held-out meeting evaluation. Dataset versions, access conditions and licenses must be checked for the exact files used.

Whisper supplies a multilingual neural transcription starting point [S02]. The platform must use original-language transcription rather than automatic translation to English, retain uncertain passages for review, and measure language-specific error. WhisperX motivates segmentation and alignment for long recordings [S03]. Word-level alignment for Kazakh is not assumed available; segment timestamps are the mandatory fallback. The pyannote pipeline illustrates speaker diarization as segmentation and clustering [S04]. A cluster label is not a verified personal identity, so names must be supplied or corrected by users.

## Meeting summarization and evidence

QMSum frames a meeting as multiple discussions from which relevant evidence must be selected [S05]. ExplainMeetSum makes the relationship between summary statements and source evidence explicit [S06]. These motivate generation from selected segments, evidence IDs on each decision or action, and source navigation in the editor. A syntactically valid source ID does not demonstrate that the source actually supports the generated statement; human entailment review remains necessary.

MeetingBank connects long transcripts with professionally prepared minutes [S07]. Its domain and language differ from the target setting, so its value is methodological: chunk long inputs, preserve source references and evaluate a structured output. Chunking can split a proposal from its later rejection. The proposed pipeline therefore retains surrounding context and performs a cross-chunk consolidation pass that preserves disagreements and corrections.

## Evaluation and unresolved limitations

SummEval supports combining automatic metrics with human assessment instead of equating lexical overlap with quality [S08]. Meeting-specific error analysis highlights omissions, attribution problems and unsupported statements [S09]. MESA explores automated quality estimation, but an LLM evaluator is not independent ground truth [S10]. The project will use two bilingual annotators, adjudicate disagreements and report both end-to-end and corrected-transcript results to separate ASR errors from generation errors.

The research gap addressed by this project is an evaluated, reviewable implementation for a defined Kazakh/Russian user setting. It is not a claim that bilingual transcription or meeting summarization is new. Local user benefit, mixed-language accuracy and hardware feasibility remain unanswered research questions.

## Structured publication analysis

| Source | Approach or finding | Limitation for this project | Design consequence |
| --- | --- | --- | --- |
| S01 KSC2, 2022 | Kazakh speech corpus with diverse sources | Not a meeting-minutes benchmark | Document data provenance; reserve in-domain meetings |
| S02 Whisper, 2023 | Multilingual weakly supervised ASR | Uneven language and domain performance | Measure WER/CER by language and noise condition |
| S03 WhisperX, 2023 | Long-audio segmentation and alignment | Alignment model coverage is language dependent | Require segment timestamps; test optional word alignment |
| S04 pyannote, 2023 | Neural diarization pipeline | Overlap and domain shift affect clustering | Anonymous labels, manual mapping and DER measurement |
| S05 QMSum, 2021 | Locate relevant discussion before summarizing | English benchmark and query-oriented task | Preserve context when selecting evidence |
| S06 ExplainMeetSum, 2023 | Evidence-aligned meeting summaries | Evidence IDs alone do not prove factuality | Human-check source support for every important item |
| S07 MeetingBank, 2023 | Long meetings aligned with professional minutes | Public council setting differs from project teams | Chunk and consolidate with traceable references |
| S08 SummEval, 2021 | Compares automatic and human evaluation | News summarization differs from meetings | Use task-level accuracy and human review |
| S09 What’s Wrong, 2025 | Identifies and refines meeting-summary errors | Refinement cannot guarantee correctness | Track omissions, invented content and wrong attribution |
| S10 MESA, 2025 | Multi-model estimation of summary quality | Judge models have their own errors | Use automated judges only as auxiliary diagnostics |

Every source is used above to change a design or evaluation decision. Full bibliographic records and direct links appear in the references chapter and docs/sources.json.

## User correction in meeting systems

Meetalk [S28] combines speech recognition with generated minutes informed by user examples and corrections. Its authors report benefits in five meeting scenarios. This supports studying a correction workflow, but the abstract does not establish Kazakh/Russian performance or justify adding personalization to the required scope. Hattama already preserves corrections and the original output; the diploma should measure whether this workflow reduces effort without losing factual quality.

| Source | Approach | Limitation for Hattama | Design use |
| --- | --- | --- | --- |
| Meetalk 2025 S28 | Generation informed by examples and user corrections | Published abstract reviewed; local bilingual generalisation not established | Evaluate corrections and reviewer effort; keep personalization optional |

## Alignment with the implementation

Whisper and pyannote papers inform alternatives and evaluation rather than describing the active default stack. Hattama currently uses mixed-CTC ASR and sherpa-onnx diarization [S33, S34]. The model and technology comparison distinguishes this implemented baseline from untested alternatives.
