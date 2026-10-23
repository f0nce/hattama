# Requirements specification

## Priority and status

This revision replaces the earlier speculative cloud design with the Hattama baseline. Must denotes the local diploma acceptance baseline, not a claim that every quality target already passes. Should denotes an extension or secondary target. Implementation status is based on source inspection and recorded evidence; experiment targets remain provisional. The existing API contract remains unchanged.

## Functional requirements

### FR-01 Local access boundary

Priority: Must. Status: Baseline.

Acceptance: The documented launcher binds the API to loopback. The UI does not claim authenticated multiuser roles. Public deployment is excluded.

Responsible component: Launch/API. Verification: T01.

### FR-02 Recording upload

Priority: Must. Status: Baseline.

Acceptance: Accept decodable WAV, MP3, M4A and FLAC with the configured default 100 MiB limit. Reject invalid input before inference; generated file paths must not use client path traversal.

Responsible component: API/audio. Verification: T02.

### FR-03 Persistent job processing

Priority: Must. Status: Baseline.

Acceptance: A valid upload returns 202 and a persisted meeting ID. A separate worker moves queued to processing and then done or failed; status remains queryable.

Responsible component: Store/worker. Verification: T03.

### FR-04 Original language transcription

Priority: Must. Status: Baseline.

Acceptance: Produce timestamped Kazakh/Russian source segments without translating all content into English. Measure linguistic quality under NFR-01; do not infer quality from schema validity.

Responsible component: ASR. Verification: T04.

### FR-05 Task source navigation

Priority: Must. Status: Baseline.

Acceptance: Each task references existing source segment IDs. Selecting evidence displays the corresponding source text; a newly edited task must retain valid sources.

Responsible component: UI/validation. Verification: T05.

### FR-06 Speaker mapping

Priority: Must. Status: Baseline.

Acceptance: Map anonymous speaker labels to supplied participants and reject duplicate ownership of one label. A label is not a verified identity.

Responsible component: Review. Verification: T06.

### FR-07 Tasks and summary

Priority: Must. Status: Baseline.

Acceptance: Return schema-valid tasks and a summary. Missing owner or deadline remains null and requires review; empty tasks are valid when no commitment is supported.

Responsible component: Pipeline. Verification: T07.

### FR-08 Result validation

Priority: Must. Status: Baseline.

Acceptance: Reject unknown sources/participants, invalid dates, duplicate IDs and invalid timestamps. Semantic support is checked by a human, not implied by validation.

Responsible component: Validation. Verification: T08.

### FR-09 Persisted corrections

Priority: Must. Status: Baseline.

Acceptance: For a done meeting, save participants, tasks and summary, increment revision and preserve edits after restart. Segments and original metadata are not editable in this API.

Responsible component: Store/review. Verification: T09.

### FR-10 Immutable machine original

Priority: Must. Status: Baseline.

Acceptance: GET original returns the unchanged machine output after any saved user correction. Store the latest correction separately; do not claim full edit history.

Responsible component: Store. Verification: T10.

### FR-11 DOCX export

Priority: Must. Status: Baseline.

Acceptance: Export one consistent saved revision containing metadata, participants, tasks, summary and transcript. Unsaved UI edits block export; fixture output is visibly labelled.

Responsible component: Export/UI. Verification: T11.

### FR-12 Meeting library

Priority: Must. Status: Baseline.

Acceptance: List saved meetings newest first and open their status/details after restart. Do not claim search or pagination absent from the API.

Responsible component: API/UI. Verification: T12.

### FR-13 Retry failed jobs

Priority: Must. Status: Baseline.

Acceptance: Only failed meetings can be requeued. Retrying queued, processing or successful meetings returns a conflict and does not discard saved successful edits.

Responsible component: Store. Verification: T13.

### FR-14 Deletion

Priority: Must. Status: Baseline.

Acceptance: Delete permitted non-processing meetings and associated audio. Reject processing deletion and do not return success if file removal fails.

Responsible component: Store/API. Verification: T14.

### FR-15 Processing visibility

Priority: Must. Status: Baseline.

Acceptance: Show actual pipeline stages and safe errors. No invented percentage or silent fallback to synthetic output is displayed.

Responsible component: Worker/UI. Verification: T15.

### FR-16 Meeting context

Priority: Must. Status: Baseline.

Acceptance: Validate title, actual meeting datetime with offset, IANA timezone and participant metadata. Reject invalid or ambiguous local datetime input in the UI.

Responsible component: API/UI. Verification: T16.

### FR-17 Concurrent review protection

Priority: Must. Status: Baseline.

Acceptance: Save against expected_revision in a transaction. A stale edit returns 409 REVISION_CONFLICT and cannot overwrite a newer saved review.

Responsible component: Store. Verification: T17.

### FR-18 Failure and fixture separation

Priority: Must. Status: Baseline.

Acceptance: A model failure yields failed status with safe details. Fixture mode is explicit configuration, visibly labelled and never an automatic error fallback.

Responsible component: Pipeline/API. Verification: T18.

### FR-19 Live meeting ingestion

Priority: Should. Status: Planned extension.

Acceptance: Before implementation agree one authorised input mode. Demonstrate ordered incremental segments, visible gaps and a reconciled final result on controlled meetings.

Responsible component: Future connector. Verification: T19.

### FR-20 Transcript editing and full revisions

Priority: Should. Status: Planned extension.

Acceptance: Persist all source/minutes revisions and invalidate derived content on a source edit. Requires a new contract; not supplied by the current latest-review store.

Responsible component: Future revisions. Verification: T20.

### FR-21 Authenticated shared review

Priority: Should. Status: Planned extension.

Acceptance: If shared deployment is approved, enforce owner/editor/reviewer/viewer permissions and revision-bound approval. Cross-meeting access tests must pass.

Responsible component: Future identity. Verification: T21.

## Nonfunctional requirements

### NFR-01 Bilingual ASR quality

Priority: Must. Status: Evaluation pending.

Acceptance: Report WER/CER separately for Kazakh, Russian and mixed held-out meetings with fixed normalization. Provisional WER targets: 25%, 20% and 30%; confirm before final testing.

Verification: E01.

### NFR-02 Minutes factuality

Priority: Must. Status: Evaluation pending.

Acceptance: Target at least 95% supported-task precision and task-tuple F1 at least 0.80 per stratum. Report omissions, incorrect owners/dates and summary errors; zero output is not perfect accuracy.

Verification: E02.

### NFR-03 Measured performance

Priority: Must. Status: Partial historical evidence.

Acceptance: Record total/stage time and memory on a named host for 1-, 10- and 30-minute inputs where feasible. Report RTF without claiming real-time speed. Establish a duration target after a pilot.

Verification: E03.

### NFR-04 API responsiveness

Priority: Must. Status: Evaluation pending.

Acceptance: During one active worker job, measure status/metadata p95 under five local clients for ten minutes; provisional target under one second excluding upload/inference.

Verification: E04.

### NFR-05 Local content processing

Priority: Must. Status: Implemented controls; OS test pending.

Acceptance: Load local weights without cloud AI fallback. Test processing under OS network isolation; distinguish library offline flags and Python socket guards from proof of full isolation.

Verification: E05.

### NFR-06 Recovery

Priority: Must. Status: Baseline tests available.

Acceptance: After interrupted processing and worker restart, interrupted jobs become visible failures and can be retried. Persisted successful reviews survive restart.

Verification: T03.

### NFR-07 Usability benefit

Priority: Must. Status: Evaluation pending.

Acceptance: In a paired study of 6–8 users, target at least 80% unaided completion and 20% lower median active time than manual preparation without lower factual quality.

Verification: E06.

### NFR-08 Usable bilingual interface

Priority: Must. Status: Evaluation pending.

Acceptance: Check keyboard reachability, labels, focus, small-screen layout and preservation of Kazakh characters in display and DOCX. Document accessibility gaps.

Verification: T22.

### NFR-09 Reproducibility

Priority: Must. Status: Baseline manifests available.

Acceptance: Each experiment records code commit, model hashes, data IDs/split, prompt/settings, hardware and result files; another member repeats one case.

Verification: E07.

### NFR-10 Recording retention

Priority: Should. Status: Policy pending.

Acceptance: Document storage location and an agreed cleanup/backup policy. Verify API deletion behavior and manual cleanup of crash remnants; no automatic 30-day backup expiry is claimed.

Verification: T14.

### NFR-11 Untrusted content handling

Priority: Must. Status: Baseline validation; adversarial tests pending.

Acceptance: Treat transcript text as data. Generation cannot execute tasks. Check escaping and malformed results; valid schema alone does not prevent misleading content.

Verification: T23.

### NFR-12 Speaker quality

Priority: Should. Status: Evaluation pending.

Acceptance: Measure DER with declared overlap treatment and a 0.25-second collar on 2–6-speaker references; proposed 20% target requires pilot review.

Verification: E08.

### NFR-13 Live latency

Priority: Should. Status: Planned extension.

Acceptance: If live ingestion is built, report audio-chunk-close-to-visible-text p95, gaps and finalization delay. Set a hardware-specific target before acceptance.

Verification: E09.
