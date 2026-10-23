# Hattama project proposal and scope

## Project identity

Development of a Platform for Automated Meeting Minutes Generation in Kazakh and Russian Using Neural Network Models

Hattama is an existing local meeting-minutes application developed during a hackathon. This diploma project extends and evaluates that application. A user uploads a recording, supplies meeting context, inspects the generated transcript and tasks, saves corrections and exports a DOCX. The first pre-defense submission combines the existing implementation with an updated research and engineering specification. Baseline source: commit 13d2271 [S35].

| Member | Diploma responsibility |
| --- | --- |
| Akhmetov Kazbek | Frontend and backend integration, recording workflow, persisted review and exports |
| Uranov Daryn | Speech and language models, diarization, evaluation data and reproducible experiments |
| Tazhibayev Marsel | Team lead, shared contracts, scope, integration, review and submission coordination |

Supervisor: Elvira Aitmukhambetovna. The team reports that the topic is agreed. University/programme details and the final defense date remain to be supplied. Individual Git accounts must be mapped to these real names by the team; this report does not infer identity from nicknames.

## Problem and target users

Meeting coordinators and secretaries need to turn discussions into accurate summaries and actionable tasks. Code-switching, overlapping speech, uncertain names and relative dates can make automatic output unreliable. Published research establishes the relevance of evidence alignment and user correction [S06, S07, S28]. The repository records an omitted deadline and an incorrect summary in one model run [S35]. The prevalence and cost of these problems among Kazakhstan users remain to be established locally.

Primary users are coordinators, secretaries and project-team members who prepare minutes on a local computer. A human checks the resulting document before sharing it. The current application has no separate authenticated reviewer or administrator accounts. Local operating-system access is the security boundary; a shared web service is outside the delivered baseline.

## Aim and objectives

The aim is to develop and evaluate an offline-capable platform that reduces active preparation effort while producing reviewable Kazakh and Russian meeting minutes.

1. Establish user needs using published evidence and actual user discussions, with assumptions explicitly separated.
2. Preserve and document the working recording-to-DOCX flow and its local processing boundary.
3. Evaluate Kazakh, Russian and mixed-speech transcription and speaker attribution on independently annotated data.
4. Compare the current generator with feasible local alternatives and an extractive baseline using the same meeting tasks.
5. Improve measured errors in task owners, deadlines, evidence references and summary faithfulness.
6. Explore live meeting ingestion only after an explicit feasibility gate; retain upload as the working baseline.

## Implemented baseline and planned development

The baseline uses React/Vite with TypeScript, FastAPI, SQLite, local audio files and a separate Python worker. The bundled pipeline uses mixed-CTC speech recognition, sherpa-onnx speaker diarization and a 4-bit Qwen3-4B-Instruct-2507 checkpoint. Mac uses MLX; the Windows path executes the quantized checkpoint through a PyTorch adapter. Weights and hashes are pinned [S21, S33–S35].

Implemented input formats are WAV, MP3, M4A and FLAC with a default 100 MiB upload limit. The application preserves the machine result and the latest saved correction. Participants, tasks and summary are editable; transcript segments and source metadata are not editable in the current review API. Export uses one saved revision. This is a useful application, not a complete multiuser approval system.

Diploma extensions prioritise bilingual evaluation, error reduction, usable review and performance measurement. Live connection is planned research/development, not an implemented feature. The earlier 500 MB/60-minute specification is superseded by the actual baseline: 100 MiB; supported recording duration must be measured rather than claimed. Native mobile apps, several meeting providers and automatic external task execution remain outside the current scope.

## Expected outcomes and engineering contribution

Expected outcomes are a reproducible Hattama release, a coherent English documentation package, editable diagrams, a traceable task/review history and a controlled evaluation of accuracy, performance and user effort. The diploma contribution builds on the hackathon baseline through documented research, verified improvements and evaluation; it must not present inherited code as newly developed work.

Engineering complexity includes process isolation, durable queued jobs, audio decoding, model orchestration, source-linked task extraction, schema validation, transactional review revisions and consistent DOCX export. Neither a larger model nor a passing interface test proves minutes quality. The first pre-defense may present implementation plus an evaluation plan without claiming completed final experiments.
