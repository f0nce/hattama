# Existing system comparison

## Method

Three relevant meeting-assistant systems are compared using ten consistent criteria. Official documentation was reviewed on 23 October 2026. This is desk research, not hands-on benchmarking. Features and plan limits can change; no quality, speed or price rankings are inferred from marketing claims.

Documented means explicitly described in the cited page. Not listed means absent from the published source-language list, not an independently tested failure. Not established means the reviewed documents do not establish the capability. The Hattama column describes the current implementation; quality is not established by feature presence.

| Criterion | Fireflies.ai | Notta | Otter.ai | Hattama baseline |
| --- | --- | --- | --- | --- |
| 1 Recording upload | Documented S12 | Documented S14 | Documented S18 | WAV, MP3, M4A, FLAC |
| 2 Kazakh source transcription | Listed S11 | Not listed S13 | Not listed S17 | Implemented; quality evaluation pending |
| 3 Russian source transcription | Listed S11 | Listed S13 | Not listed S17 | Implemented; quality evaluation pending |
| 4 Kazakh–Russian mixed speech | Exact pair not established S11 | Kazakh not in bilingual source list S14 | Neither source language listed S17 | Required evaluation stratum |
| 5 Summary and action items | Documented S12 | AI Notes and tasks S15 | Documented S19 | Structured draft with unknown fields |
| 6 Editable generated content | Not established in reviewed pages | AI Notes editable S15 | Conversations editable S18 | Participants, tasks and summary |
| 7 Export | Download documented S12 | Notes export S16 | Export documented S18 | DOCX export; JSON via API |
| 8 Item-level source evidence | Not established | Not established | Not established | Task source IDs validated; summary support needs review |
| 9 Revision and approval control | Not established | Not established | Not established | No formal approval; save conflict check |
| 10 Self-managed inference deployment | Not established | Not established | Not established | Implemented local model stages |

Notta's Kazakh translation target must not be confused with Kazakh audio transcription support [S13]. Fireflies already lists both target languages [S11]; therefore the title's language pair alone is not a defensible uniqueness claim. “Not established” cells must not be presented as missing product features.

## Rationale for the proposed solution

The project combines task source links, unknown-value handling, a preserved machine original and local neural processing. A language-stratified evaluation will assess its practical value. Interviews must establish whether those priorities solve a meaningful local problem. A matched manual workflow is the feasible primary baseline; competitor benchmarking would require comparable access, consent and test conditions and is optional.

A follow-up product audit should record plan, product version, test recording, language mode and observed result. It should revisit undocumented cells before any claim of superiority is made. The system comparison is sufficient to motivate design choices, not to prove market demand.
