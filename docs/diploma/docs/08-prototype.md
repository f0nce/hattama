# Working interface and demonstration

## Existing application

The repository contains the actual React interface integrated with FastAPI and the local worker. It supersedes the earlier stand-alone fictional prototype for the primary demonstration. No application rewrite is required. Use README.md at repository root for the operating-system-specific setup and launch steps.

The main journey is uploaded audio → actual processing stages → source-linked tasks and summary → saved corrections → DOCX. The meeting library retains records across restart. The current API permits editing participants, tasks and summary, not transcript text. There is no final approval button backed by a role model and no real-time meeting connection.

## Demonstration script

1. Launch Hattama using the documented Mac or Windows profile and open the loopback interface.
2. Upload a short permitted recording; supply its actual date, time zone and participants. Select a language-appropriate example.
3. Show queued/processing and the actual pipeline stage. Explain that inference is local and timing depends on hardware.
4. Open a generated task and its source segment. Check speaker attribution, owner and date; explain unknown fields.
5. Correct the summary or task, save it and inspect the immutable original separately.
6. Download DOCX and confirm the saved correction and Kazakh characters. Reopen the meeting after restart.
7. State measured limitations, including errors observed in the recorded run and the absence of live connection.

Keep a preprocessed permitted example ready so a long model run does not consume the whole presentation. State clearly if a result was prepared before the demonstration. The fixture profile is useful for interface checks only; it must remain visibly labelled synthetic.

## Interface evidence and checks

| Interface area | User action | Verification |
| --- | --- | --- |
| Upload/context | Select audio and meeting metadata | Invalid/oversized input rejected; no file-path trust |
| Processing | Follow real stages | Failure visible; no invented progress percentage |
| Review | Inspect sources and edit permitted fields | Original preserved; stale revision rejected |
| Library | Reopen saved meeting | Saved review survives restart |
| Export | Save and download DOCX | Export reflects saved revision; unsaved edits blocked |

The repository includes historical browser/HTTP/export checks. The updated report identifies these as recorded evidence rather than claiming a new full-model demonstration in this editing session. A final rehearsal on the presentation machine remains necessary. The committee can view the existing application; an additional mock interface is unnecessary.
