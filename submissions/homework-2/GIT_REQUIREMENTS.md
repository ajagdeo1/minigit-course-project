# Homework 2 — Part 2 Submission

Student name: Adrian Jagdeo

GitHub username: ajgdeo1

## 1. Git Command Observations

| Command or workflow | What did you observe? | What was the user trying to accomplish? | What problem or risk did it address? |
|---|---|---|---|
| 1. git status |Used to display modified and staged filed| Understand the current status of the local repo|Helps keep track of files across the repo to prevent any mistakes such as making incorrect commits|
| 2. git diff | Observed: Shows modified lines between the working directory and the last snapshot | Allows you to review any edits before committing | Helps with identifying mistakes |
| 3. git add [file] followed by git diff –staged | Stages a file to be committed and shows what changes will be included in the new snapshot | Stage specific modifications and verify those changes before committing | Makes sure the desired changes are implemented and does not include incomplete files |
| 4. git commit -m followed by git log –oneline | Creates a snapshot followed by a brief descriptive message of modifications followed by a log of previous commits and the messages attached to them. | Record modifications and identify those modifications | Provides a history of the project and allows points of restoration |

## 2. User Needs

### UN-GIT-01 — Understand Modifications

> An intern needs to be able to identify what files have been modified and what changes were done to the files compared to the previously recorded snapshot because they need to be able to review the changes in order to catch any potential mistakes.

### UN-GIT-02 — Record and View History

> A developer needs a way to record major project contributions and review it and other changes because people working on teams need a way to view the project's progress and the ability to revert to a more stable version.


### UN-GIT-03 — Select Specific Modifications

> A developer needs a way to select specified files with finished work because incomplete modifications can lead to confusion on a team or bugs that may be difficult to identify.

## 3. User Requirements

| ID and short title | User requirement | Source user need | Rationale |
|---|---|---|---|
| UR-GIT-01 View modifications | An intern shall be able to view modified before creating a save of that new version | UN-GIT-01 | Allows the user to understand the details of the modifications |
| UR-GIT-02 Check logs | A developer shall be able to review saved versions along with a message of those modifications | UN-GIT-02 | Allows a traceable history to be reviewed and used for recovery |
| UR-GIT-03 Verify specified changes | A developer shall be able to view the specific changes be submitted to the new snapshot before committing to any changes | UN-GIT-03 | Prevents the developer from including any unrelated modifications |
| UR-GIT-04 Select specific files for changes | A developer shall be able to select what files are to be included into the new saved version  | UN-GIT-03 | Allows developers to make working contributions while leaving out items that still need work |

