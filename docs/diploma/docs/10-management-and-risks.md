# Project management and risks

## Repository and inherited baseline

The project repository is https://github.com/f0nce/hattama. The hackathon baseline is commit 13d2271. History already contains contributions and references to PRs in the former BAITC-Hacks repository. Those messages do not prove that review comments are available in the new repository. Preserve history, retain accessible provenance links and identify the new diploma work explicitly.

The diploma documentation update is developed in a separate branch and submitted through a PR. main remains the reviewed baseline. Another team member should review before merge. No completed review, individual student authorship, YouTrack issue ID or submission tag is fabricated. Existing Git author identity is used transparently for the documentation contribution.

YouTrack has been created according to the team. Its URL and access are not available for this update. The local backlog remains a planning file until mapped to real issues. Do not treat PLAN IDs as live issue IDs or silently count this rubric item as complete.

## Team and milestones

| Member | Responsibility | Review contribution |
| --- | --- | --- |
| Akhmetov Kazbek | UI, API, saved review and DOCX workflow | Review model-output integration |
| Uranov Daryn | Models, datasets, metrics and error analysis | Review bilingual evidence and experiments |
| Tazhibayev Marsel | Scope, shared contracts, integration and release | Coordinate cross-component review |

| Milestone | Proposed date | Exit condition |
| --- | --- | --- |
| First pre-defense package | 24 October 2026 | Aligned report/deck, diagrams, task plan and honest evidence status |
| Discovery and evaluation protocol | 6 November 2026 | User findings or approved alternative, data permission, frozen definitions |
| Baseline evaluation | 27 November 2026 | Same-data ASR/generation results and documented failure cases |
| Measured improvements | 18 December 2026 | Reviewed fixes or model selection supported by comparisons |
| Usability and robustness | 22 January 2027 | Paired user study and reproducible system checks |
| Final defense | Not supplied | Confirm academic date and final acceptance scope |

Dates are proposed and must be reconciled with the university calendar. Live integration starts only after its feasibility and acceptance scope are approved; it does not delay documentation of the working upload baseline.

## Risks and dependencies

| Risk | Owner | Likelihood and impact | Mitigation and trigger |
| --- | --- | --- | --- |
| Kazakh or mixed-speech errors | Daryn | High / high | Separate language strata; inspect corrections before changing models |
| Invented or omitted owner/date | Daryn | High / high | Source references, null fields and human review; measure both precision and recall |
| Larger model exceeds hardware | Daryn | High / medium | Resource gate; keep Qwen baseline and disclose infeasible candidates |
| Live mode expands scope | Marsel | Medium / high | One connector; explicit future status and feasibility decision |
| Conflicting review saves | Kazbek | Medium / high | expected_revision transaction and regression tests |
| Recorded meetings lack publication permission | Marsel | Unknown / high | Verify provenance and permitted use; do not assume hackathon access permits public reuse |
| Missing YouTrack access | Marsel | High / medium | Preserve backlog locally and map real issues when access returns |
| Missing user/supervisor evidence | Marsel | High / high | Clearly labelled draft materials; collect actual evidence or documented assessment exception |
| Demo environment differs | Kazbek | Medium / high | Rehearse on target host, keep a disclosed preprocessed example |

## Work traceability and submission

Every substantive item needs an owner, outcome, acceptance criteria and deadline. Once tracker access is available, create real issues and use their IDs in task branches/PRs. Link PRs back to tasks and record who checked each criterion. Do not backdate issues or divide generated files into artificial student contributions.

After peer review and merge, tag the exact accepted commit as pre-defense-1. Later tags must identify later exact versions without moving earlier tags. Provide URL, tag, completed work, limitations and outstanding tasks. A PR is reviewable work, not a completed peer review or final submission tag.
