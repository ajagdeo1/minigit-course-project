## Approved UN/UR Baseline

# Approved MiniGit user needs and user requirements

This instructor-approved baseline is the starting point for Homework 3. Homework 2 was practice; students should keep their HW2 work, but use the stable IDs below for HW3–HW6. These statements describe the user's goal and visible capability. They do not specify storage files, hashing, classes, or algorithms.

## Project boundary

MiniGit is a local educational version-control tool. It supports `init`, `status`, `diff`, `diff --staged`, `add <file>`, `commit -m <message>`, and `log`. It does not implement branches, merging, network operations, GitHub, or Pull Requests. Students use real Git/GitHub for class collaboration.

## User needs

| ID | Stakeholder need |
|---|---|
| UN-GIT-01 | A student developer needs a way to start tracking a local project because it has no recorded history. |
| UN-GIT-02 | A student developer needs to know which project files have changed because they may forget what they edited before recording a checkpoint. |
| UN-GIT-03 | A student developer needs to inspect changed content before recording it because a file may contain unintended edits. |
| UN-GIT-04 | A student developer needs to choose the file content to include in the next checkpoint because later edits may still be unfinished. |
| UN-GIT-05 | A student developer needs to record a meaningful checkpoint because they want to preserve a known project state and explain its purpose. |
| UN-GIT-06 | A student developer needs to review earlier checkpoints because they want to understand how the project reached its current state. |
| UN-GIT-07 | A student developer needs invalid commands to explain why they failed while preserving existing project files and recorded checkpoints. |

## User requirements

| ID | User-visible capability | Need |
|---|---|---|
| UR-GIT-01 | A student developer shall be able to initialize tracking in the current local project folder without removing existing project files. | UN-GIT-01, UN-GIT-07 |
| UR-GIT-02 | A student developer shall be able to see whether project files are untracked, staged, changed after staging, modified, deleted, or clean. | UN-GIT-02 |
| UR-GIT-03 | A student developer shall be able to view differences between current working file content and the content selected for the next checkpoint. | UN-GIT-03 |
| UR-GIT-04 | A student developer shall be able to view differences between content selected for the next checkpoint and the latest recorded checkpoint. | UN-GIT-03 |
| UR-GIT-05 | A student developer shall be able to select the current content of one existing project file for the next checkpoint without selecting unrelated files. | UN-GIT-04 |
| UR-GIT-06 | A student developer shall be able to create a checkpoint of selected content with a nonempty explanation while leaving later unselected edits in the working files. | UN-GIT-05, UN-GIT-04 |
| UR-GIT-07 | A student developer shall be able to view recorded checkpoints from newest to oldest, including their identifier and explanation. | UN-GIT-06 |
| UR-GIT-08 | A student developer shall receive a useful error when a command is invalid, a requested file is unavailable, or a path is outside the allowed project files. | UN-GIT-07 |
| UR-GIT-09 | A student developer shall be able to retry an operation after a failure without losing ordinary project files or an already recorded checkpoint. | UN-GIT-07 |

## Worked relationship example

`UN-GIT-04` explains why selection matters. `UR-GIT-05` grants the user the capability to select one current file. A student may derive a system requirement that `add <file>` copies that file's current content into a stage area and does not include another file. They may then write an acceptance test that stages `notes.txt`, edits it again, and checks that the staged copy still contains the earlier content. The system requirement and test are examples of the next level; they are **not** part of this approved user baseline.

## Clarification of UN-GIT-07

This need concerns **failure handling before a mistaken command takes effect**, not an `undo`, `revert`, or restore feature. For example, `add missing.txt` should report an error without changing an existing staged copy; `commit -m ""` should report an error without changing the latest checkpoint. The user may correct the input and retry. Recovering an earlier file version after a successful commit is outside this MiniGit scope.

## Baseline use rules

1. Copy these nine UR IDs and seven UN IDs into the HW3 baseline section without renumbering.
2. A system requirement may support more than one UR; every UR must have at least one supporting system requirement.
3. Derive observable system behavior and verification; do not copy a UR and merely replace “student developer” with “system.”
4. If a student identifies a genuine ambiguity, record a proposed clarification and use the instructor's approved wording for grading until a published update is issued.

## UR-to-UN Mapping

UR-GIT-01 → UN-GIT-01, UN-GIT-07
UR-GIT-02 → UN-GIT-02
UR-GIT-03 → UN-GIT-03
UR-GIT-04 → UN-GIT-03
UR-GIT-05 → UN-GIT-04
UR-GIT-06 → UN-GIT-05, UN-GIT-04
UR-GIT-07 → UN-GIT-06
UR-GIT-08 → UN-GIT-07
UR-GIT-09 → UN-GIT-07

## Functional System Requirements

SR-01 first init
SR-02 repeated init
SR-03 add one existing file
SR-04 add a missing file
SR-05 status for one staged file
SR-06 status for modified after staging
SR-07 diff from working to staged
SR-08 diff from staged to latest checkpoint
SR-09 commit selected content
SR-10 empty commit message rejected
SR-11 log newest to oldest
SR-12 invalid command leaves state unchanged

1. SR-01 (source UR-GIT-01): Given a local project folder containing notes.txt with content ONE and no existing MiniGit tracking, when `init` is used, MiniGit shall initialize tracking without changing or removing notes.txt.
   Check: Inspect notes.txt after `init`; it still contains ONE.

2. SR-02 (source UR-GIT-01, UR-GIT-08): Given a project that has already been initialized and contains notes.txt with content ONE, when `init` is used again, MiniGit shall display a useful error that tracking already exists and shall leave notes.txt unchanged.
   Check: Inspect the command output and notes.txt; the error is shown and notes.txt still contains ONE.

3. SR-03 (source UR-GIT-05): Given an initialized project with notes.txt containing ONE and plan.txt present, when `add notes.txt` is used, MiniGit shall stage a copy of notes.txt containing ONE without staging plan.txt.
   Check: Inspect staged content; notes.txt contains ONE and plan.txt is not staged.

4. SR-04 (source UR-GIT-08, UR-GIT-09): Given an initialized project with notes.txt already staged containing ONE, when `add missing.txt` is used and missing.txt does not exist, MiniGit shall display a useful unavailable-file error and keep the staged copy of notes.txt containing ONE.
   Check: Inspect the error output and staged notes.txt; the error is shown and notes.txt still contains ONE.

5. SR-05 (source UR-GIT-02): Given an initialized project with notes.txt staged and unchanged after staging, when `status` is used, MiniGit shall show that notes.txt is staged.
   Check: Inspect the status output; it identifies notes.txt as staged.

6. SR-06 (source UR-GIT-02, UR-GIT-03): Given an initialized project with notes.txt staged containing ONE and then edited in the working files to TWO, when `status` is used, MiniGit shall show that notes.txt is modified after staging.
   Check: Inspect the status output; it identifies notes.txt as changed after staging and not clean.

7. SR-07 (source UR-GIT-03): Given an initialized project with notes.txt staged containing ONE and then edited in the working files to TWO, when `diff` is used, MiniGit shall display the difference between the current working file content and the staged content.
   Check: Inspect the diff output; it shows the change from ONE to TWO without showing unrelated files.

8. SR-08 (source UR-GIT-04): Given an initialized project with notes.txt staged containing ONE and a previously recorded checkpoint containing ZERO, when `diff --staged` is used, MiniGit shall display the difference between the staged content and the latest recorded checkpoint.
   Check: Inspect the diff output; it shows the staged content relative to the latest checkpoint and indicates the change from ZERO to ONE.

9. SR-09 (source UR-GIT-06): Given an initialized project with notes.txt staged containing ONE and a nonempty commit message `first checkpoint`, MiniGit shall record a new checkpoint containing the staged content and shall leave later unselected edits in the working files unchanged.
   Check: Inspect the recorded checkpoint and working files; the new checkpoint contains ONE, the message is recorded, and any other edited file remains uncommitted.

10. SR-10 (source UR-GIT-06, UR-GIT-08): Given an initialized project with notes.txt staged containing ONE and the user attempts `commit -m ""`, MiniGit shall reject the command with a useful error and shall not create a new checkpoint or remove the existing staged content.
   Check: Inspect the command output and stored checkpoint list; the error is shown and no checkpoint is added while notes.txt remains staged.

11. SR-11 (source UR-GIT-07): Given at least two recorded checkpoints in an initialized project, when `log` is used, MiniGit shall list checkpoints from newest to oldest, including each checkpoint identifier and its commit explanation.
   Check: Inspect the log output; it shows the newest checkpoint first and includes both the identifier and message for each entry.

12. SR-12 (source UR-GIT-08, UR-GIT-09): Given an initialized project and a command such as `add missing.txt`, `commit -m ""`, or a request for a file outside the project, when the command is invalid, MiniGit shall display a useful error and leave existing project files and recorded checkpoints unchanged.
   Check: Inspect the error output and the project state; the invalid command fails without altering ordinary files or the latest recorded checkpoint.