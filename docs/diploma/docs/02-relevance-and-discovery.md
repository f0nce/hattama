# Relevance and evidence of user needs

## Evidence that is available

Three forms of evidence are kept separate: published studies, repository observations and direct user discovery. The topic agreement is reported by the team. No completed local interviews or client agreement have been supplied. The team reports permission to use constructed examples; such examples below are labelled illustrative and are not participant testimony. If the committee accepts an alternative to its written interview requirement, retain that explicit decision.

| Evidence | Verified observation or author report | Project implication and limit |
| --- | --- | --- |
| Meetalk 2025 [S28] | Authors describe ASR plus generated minutes adapted through user examples/corrections and report a user study in five meeting scenarios | Supports editable drafts and review cues; does not prove Kazakhstan user demand or Hattama quality |
| MeetingBank 2023 [S07] | Professional minutes are aligned with segments of public council meetings | Supports source-linked output and long-recording evaluation; language and setting differ |
| ExplainMeetSum 2023 [S06] | Meeting summaries are connected to supporting evidence | Motivates source references; a valid source ID alone does not establish truth |
| Hattama recorded Windows run [S35] | One synthetic Russian input produced an omitted relative deadline and an incorrect summary | Demonstrates an actual failure mode in this implementation; one run is not a prevalence estimate |

Meetalk is used at the level supported by its published abstract; this package does not claim an independent replication. Literature supports the design rationale. Local efficiency gains, preferred output format and willingness to use the platform remain hypotheses.

## Illustrative scenarios for requirements discussion

The following are constructed design scenarios, not interviews, quotations or measured observations.

1. A university coordinator reviews a mixed-language meeting. A task says that a document is needed by the following day, but the generator omits the date. The user checks the cited segment and supplies the verified deadline.
2. A project-team secretary sees a speaker label assigned to the wrong participant. The user remaps the label, verifies task owners and saves the correction before DOCX export.
3. A local administrator requires recording contents to remain on the workstation. Dependencies and model weights are prepared beforehand, and inference is tested with networking disabled.

These scenarios motivate FR-06, FR-08, FR-09 and NFR-05. They must not be counted as completed discussions or used to claim time savings.

## Primary evidence still to collect

Recruit 3–5 distinct user representatives: two coordinators/secretaries, one meeting chair, one bilingual participant and, if available, an information owner. Discuss the most recent actual meeting before showing the interface. Ask how minutes were prepared, what was corrected, which languages were used, how deadlines were resolved and what sharing restrictions applied. Record actual dates, roles, consent and counterexamples.

Use the interview template and evidence register. Link each finding to a requirement change. A written exchange can provide useful evidence if substantive and accepted by the supervisor; the team must not assume that fictional scenarios meet the original rubric. If an alternative assessment route is permitted, record who authorised it and what evidence is required instead.

## Hypotheses to test

| Hypothesis | Evidence required | Decision affected |
| --- | --- | --- |
| Review takes less active time than manual preparation | Paired user study with quality guardrail | NFR-07 usability benefit |
| Mixed speech increases correction effort | Annotated language spans and observed corrections | Model selection and evaluation strata |
| Users need traceable task sources | Actual disputed-task examples | FR-05 and FR-08 evidence workflow |
| Offline processing matters to the target setting | Stated data-handling constraints | Local deployment boundary |
