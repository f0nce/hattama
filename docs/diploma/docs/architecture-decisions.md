# Architecture decisions

ADR-01 Retain the existing React/Vite client and FastAPI API. Reason: working integrated baseline and Python model interface. Revisit only with a demonstrated requirement.

ADR-02 Retain SQLite and local files for a trusted workstation with one worker. PostgreSQL/object storage is a future multiuser option, not the delivered implementation.

ADR-03 Keep inference in a separate worker and heavy stages in child processes. The API remains responsive; short database transactions protect job/review state.

ADR-04 Keep local model inference without cloud fallback. Retain the pinned mixed-CTC, sherpa and Qwen3-4B baseline; evaluate alternatives before replacement.

ADR-05 Preserve machine original and latest saved review. Full edit history and formal role-bound approval require a new design and are not claimed by revision counters.

ADR-06 Keep upload as the implemented input. Live meeting capture remains a separately evaluated extension. This supersedes the earlier proposed cloud architecture without changing application code.
