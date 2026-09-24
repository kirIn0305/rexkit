# Experiment Queue

This page lists all recorded work, including research experiments, environment setup, investigations, implementations, and bug fixes.

Each Experiment's README contains its instructions, progress, execution details, and results. See [the workflow](../docs/WORKFLOW.md) for how Experiments are created and managed.

Creating an Experiment is optional. Ask the user before recording work as a new or existing Experiment unless they have already specified their choice.

## Ready

Prepared for the next actor to review or execute. `ready` does not mean that a restricted operation has been approved.

| Priority | ID | Next action | Owner | Resources | Command or link |
|---:|---|---|---|---|---|
| 1 | [EXP-001](EXP-001_short-name/README.md) | Review and run | human | TBD | `bash experiments/EXP-001_short-name/run.sh` |

<!-- Remove the example row when using this template. -->

## In progress

| ID | Work | Owner | Current state | Next action |
|---|---|---|---|---|
| — | — | — | — | — |

## Planned

| Priority | ID | Work | Related RQ | Next action |
|---:|---|---|---|---|
| — | — | — | — | — |

## Blocked

| ID | Work | Blocker | Needed to resume |
|---|---|---|---|
| — | — | — | — |

## Completed

| ID | Work | Outcome | Result |
|---|---|---|---|
| — | — | — | — |

## Cancelled

| ID | Work | Reason |
|---|---|---|
| — | — | — |

## Maintenance

- Assign the next unused `EXP-xxx` ID when creating an Experiment.
- Keep each Experiment in exactly one status section.
- Update this page when an Experiment's status or next action changes.
- Put detailed instructions, commands, logs, and measured values in the Experiment README; keep this page brief.
- For work that requires a run, identify the execution owner as `agent`, `human`, or `hybrid` in the Experiment README.
- Do not treat a command listed here as authorization to execute it. Check `AGENTS.md` and the Experiment README before running restricted operations.
