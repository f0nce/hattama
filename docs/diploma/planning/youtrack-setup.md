# YouTrack team quick start

The team reports that one member has already created YouTrack; access is currently unavailable. Its URL, project and permissions have not been inspected. Use the existing instance; all three members should join the same project with their own accounts.

## Invite the team

The owner opens Projects → the project → Settings → People → Add people, enters the other members' email addresses, enables Add to team and selects Invite. Each recipient accepts the email invitation. Existing users can be selected directly. Menu labels depend on the installed version. If settings or invitations are unavailable, use the instance administrator; creating new accounts may require User Manager/Create User permission in addition to project access.

Use Contributor for ordinary team work and Project Admin for the person managing project settings. A supervisor who needs to comment can receive appropriate project permissions. Observer alone is not a project-reading role. Verify access using each person's account.

Sources: [Project membership](https://www.jetbrains.com/help/youtrack/cloud/manage-project-access.html), [Default roles](https://www.jetbrains.com/help/youtrack/cloud/default-roles.html), checked 23 October 2026.

## Create the first issue together

Open Issues → New issue, select the project, enter Summary and Description, set available fields and click Create. Choose a real Assignee and a Priority. Add a Due Date field through the project administrator if the project does not expose it. The project configuration controls the available fields.

[Official issue guide](https://www.jetbrains.com/help/youtrack/cloud/create-and-edit-issues.html).

Suggested first task:

Summary: Configure team access and project tracking

Expected outcome: All three students can access the same project and use its tasks.

Acceptance criteria:
- All three individual accounts can open the project.
- Each member can be assigned an issue.
- A test issue has an owner, priority and deadline.
- README contains the real repository and tracker links.
- Another team member verifies the result and records a review comment.

Assign this setup task to the member who created the instance. Select a real agreed deadline. This is a task example, not a claim that setup is complete.

## Use the 33-task backlog

backlog.csv contains the prepared summaries, descriptions, planned owners, priorities and proposed dates. For a small team, manually create the first few issues together, then divide the remaining entry work. Avoid duplicate issues. Use task-id-mapping.md to map each PLAN identifier to its real issued identifier and URL. Planned owner is text, not an actual Assignee; choose the person's account separately. Reconcile all dates with the academic schedule.

Optional bulk import uses CSV → Google Sheets → YouTrack. The official route requires additional import permissions and configuration, so it is not necessary for the first setup session. Follow the [official import guide](https://www.jetbrains.com/help/youtrack/cloud/import-from-csv.html) if choosing that route. Do not import until you understand the destination and account mapping.

## Daily team workflow

Agree a simple sequence such as Open → In Progress → Review → Done. These are proposed states; use existing equivalent values or ask the project administrator to configure them. Move a task to In Progress when work starts. Add the artifact or PR link when ready. A second member checks the acceptance criteria and leaves a concrete review comment; mark Done only after the criteria are met and review is complete. A board is optional: the issue list is sufficient to start.

Use the real issued ID in branch names and PRs. Example only: if YouTrack issues MIN-12, use branch MIN-12-literature-review, reference MIN-12 in the PR and paste the PR link into that issue. This works manually without setting up a GitHub integration.

For the committee, demonstrate one complete task → artifact/PR → review chain. Task descriptions belong in YouTrack; versioned documents and code belong in the repository. Keep the two connected by links.
