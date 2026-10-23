# Hattama architecture and data design

## Current system boundary

The architecture describes source commit 13d2271. A local browser runs React/Vite and calls FastAPI on loopback. SQLite stores meetings, jobs and reviews; local files hold recordings. A separate Python worker calls ai.pipeline.run_pipeline(input_data, on_progress=None). Model stages run locally in child processes. There is no Redis, Celery, PostgreSQL, S3 service, SSE or live meeting connector in this baseline [S35].

The user uploads, reviews and exports on the same trusted workstation. Human review is a workflow action; it is not a separately authenticated approval role. Downloaded dependencies and prepared model weights are deployment inputs, not inference-time cloud services.

## Components and processing

| Component | Implemented responsibility |
| --- | --- |
| frontend | Recording/context form, meeting list, status polling, participant/task/summary review and export controls |
| backend/app.py | HTTP validation, upload limit, routes, safe errors and static frontend serving |
| backend/store.py | SQLite transactions, queued jobs, original/latest-review data and revision conflicts |
| backend/worker.py | Single worker ownership, recovery and calling the AI pipeline |
| ai | Audio preparation, ASR, diarization, alignment, task/summary extraction and validation |
| backend/export.py | DOCX from one saved review revision |
| scripts and model manifests | Installation, launch, pinned weight assembly and checks |

A validated upload creates queued state. The worker claims work with BEGIN IMMEDIATE, then runs inference outside the database transaction. Progress stages are preparing_audio, transcribing, diarizing, aligning, extracting_tasks, summarizing and validating. Summary and tasks are generated together. Success becomes done; an exception becomes failed. On worker restart, abandoned processing records become failed instead of silently pretending completion.

## Data and revisions

The default application directory is .local/app. The database holds meeting context, state, stage, safe error information, original_json, review_json and a revision number. Audio files use server-generated paths. Result objects contain participants, timestamped segments, tasks, summary and warnings. Each task has source_segment_ids; unknown owner/date values remain null.

PUT review replaces participants, tasks and summary for a done meeting. Source segments and meeting metadata are immutable in this endpoint. expected_revision is checked transactionally; a concurrent outdated edit receives 409. The machine original remains unchanged. Only the latest saved review is retained; a revision counter is not a full historical log. A formal approval state is not implemented.

## API summary

| Method and path | Behavior |
| --- | --- |
| POST /api/v1/meetings | Validate audio/context; persist a queued meeting; return 202 |
| GET /api/v1/meetings | List summaries without full result content |
| GET /api/v1/meetings/{id} | Return current status and result when done |
| GET /api/v1/meetings/{id}/original | Return immutable machine output |
| PUT /api/v1/meetings/{id}/review | Save permitted fields with expected_revision |
| POST /api/v1/meetings/{id}/retry | Requeue failed only |
| DELETE /api/v1/meetings/{id} | Remove non-processing meeting/audio; reject processing deletion |
| GET /api/v1/meetings/{id}/export.docx | Export one consistent saved revision |

The authoritative HTTP contract is contracts/API.md at repository root. This diploma document introduces no new routes or schema fields.

## Reliability and local processing

Single-worker locking prevents concurrent consumers for one database. Each heavy AI stage is a child process, allowing memory release between stages. Recorded Windows behavior uses an MLX-format 4-bit checkpoint through the PyTorch adapter. Current context/output limits are application settings and are lower than the upstream Qwen maximum.

Offline flags, local-only FFmpeg protocols and Python socket guards reduce accidental network use. They do not replace an OS network-isolation test. The baseline has no public authentication or encrypted local storage. Keep deployment on loopback and document access/retention expectations. Recordings and protocol files inherited under data/ require permission review before public redistribution; no existing data is removed by this documentation update.

## Planned extensions

Live ingestion, editable source transcripts with full revision history and authenticated shared approval are shown in the requirements as extensions, not inserted into current architecture diagrams. A future connector must preserve the local inference boundary and define buffering, gaps, ordering and final reconciliation. New contracts require explicit design and review before implementation.
