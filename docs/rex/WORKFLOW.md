# Research Workflow

This document describes how humans, ChatGPT, Claude Code, GitHub Copilot, and other agents collaborate in this repository.

The repository is the primary record of research decisions, work, and results.
Its contents may be incomplete or incorrect. Verify important claims against
the implementation, configuration, tests, and observed results.
See the root `AGENTS.md` for mandatory rules for AI agents.

## 1. Roles

| Actor | Primary responsibilities |
|---|---|
| Human | Final research decisions, approvals, reviews, and experiment execution when appropriate |
| ChatGPT | Research discussion, hypothesis refinement, experiment design, and result interpretation |
| Claude Code or another coding agent | Code investigation, implementation, testing, experiment preparation, and authorized execution |
| GitHub Copilot | IDE-based completion, small edits, and test assistance |
| GitHub | Version control for research records, code, Experiments, and results |

These are responsibilities, not fixed permissions. The execution owner is chosen for each Experiment.

## 2. Where information belongs

| Location | Purpose |
|---|---|
| `README.md` | Project overview and entry point |
| `AGENTS.md` | Mandatory rules for AI agents |
| `docs/rex/WORKFLOW.md` | This workflow |
| `docs/rex/templates/EXPERIMENT.md` | Template for Experiment overviews and research results |
| `docs/rex/templates/TASK.md` | Template for Experiment requests, work instructions, execution, and handoff records |
| `research/README.md` | Research goals, Research Question list, and overall timeline |
| `research/RQ-xxx.md` | Hypotheses, evidence, interpretations, and open questions for each RQ |
| `experiments/README.md` | Work index and queue of Experiments ready to run |
| `experiments/EXP-xxx_name/README.md` | Objective, background, hypothesis, method, results, and interpretation for one Experiment |
| `experiments/EXP-xxx_name/TASK.md` | User request, work instructions, acceptance criteria, execution, progress, validation, and handoff |

Write the contents of documents under `research/` and `experiments/` in Japanese. Preserve code, commands, paths, identifiers, proper nouns, and quoted source text in their original form when translation would reduce accuracy.

Avoid copying the same information into multiple places. Link to its source of truth instead.

## 3. Research cycle

1. The human and ChatGPT discuss an RQ, hypotheses, and existing results.
2. They identify uncertainties and alternative explanations.
3. They design the next Experiment when needed.
4. The human decides whether to record the work as an Experiment.
5. The assigned actor implements or prepares the work and runs low-cost validation.
6. An execution owner is selected for the Experiment.
7. The work is executed and evaluated within the approved scope.
8. Results are recorded in the Experiment.
9. The human and ChatGPT interpret the results and update the RQ.

Research discussion alone does not automatically create files or Experiments.

## 4. Discussing RQs and hypotheses

Before discussing a specific RQ, review:

- `research/README.md`
- The relevant `research/RQ-xxx.md`
- `experiments/README.md`
- Related completed Experiments

Separate direct observations, interpretations, hypotheses, and speculation. When a result does not support a hypothesis, consider what it rules out and what should be tested next.

Example prompt for ChatGPT:

> Review the target RQ and related Experiments. Summarize the direct observations, currently supported hypotheses, remaining uncertainties, and alternative explanations. Do not modify files yet.

## 5. Moving from chat to repository work

The user may give a short instruction in chat, such as “Set up the environment,” “Investigate this code,” or “Add this feature.” The user does not need to write an instruction document first.

If the user has not specified how the work should be recorded, the agent asks before modifying files:

> Should I record this as a new Experiment, add it to an existing Experiment, or proceed without an Experiment?

The agent does not create an Experiment or modify repository files until the user chooses. If the user has already specified an Experiment or chosen not to create one, do not ask again.

Do not ask this question for explanations, brainstorming, research discussions, status checks, or ideas that the user has not decided to implement.

Recommend recording the work as an Experiment when it spans multiple sessions, needs validation, affects a research decision, may require a handoff, or must be reproduced later. The user makes the final choice.

## 6. Creating an Experiment

When the user chooses to create a new Experiment, the agent:

1. Checks existing IDs in `experiments/README.md`.
2. Reads `docs/rex/templates/EXPERIMENT.md` and `docs/rex/templates/TASK.md`.
3. Creates `experiments/EXP-xxx_short-name/` using the next available ID.
4. Creates its `README.md` from the Experiment template.
5. Creates its `TASK.md` from the Task template.
6. Preserves the original request under `ユーザーの依頼` in `TASK.md`.
7. Links the relevant RQ, if any, from `README.md`.
8. Adds the Experiment to `experiments/README.md`.
9. Records a work plan in `TASK.md` before starting the work.

Use `TBD` for undecided information and `N/A` for sections that do not apply. Do not invent conditions or metrics that would materially affect the result.

Environment setup, investigation, implementation, and bug fixes can all be managed as Experiments. Do not create unnecessary scripts or configuration files merely to fill out a template.

## 7. Status and queue

| Status | Meaning |
|---|---|
| `planned` | Defined but not started |
| `in_progress` | Investigation, implementation, or execution is underway |
| `ready` | Ready for the next actor to execute or review |
| `blocked` | Waiting for a decision, permission, environment, or resource |
| `completed` | Acceptance criteria are met and required results are recorded |
| `cancelled` | Intentionally stopped |

If code and execution scripts are ready but the main run remains, mark the Experiment `ready`, not `completed`.

`experiments/README.md` should show work that is in progress, ready to run, planned, blocked, and completed. For ready-to-run Experiments, include the command, required resources, and output location when known.

## 8. Implementation and preparation

When assigning an Experiment to Claude Code or another coding agent, identify its directory:

> Read `AGENTS.md` and the target Experiment's `README.md` and `TASK.md`. Confirm the objective, constraints, and acceptance criteria, then record a work plan in `TASK.md`. Implement the change, run relevant tests and a reduced-cost smoke test where possible, and record the results and remaining work.

Before making changes, the assigned actor inspects the existing code and tests and limits the scope of the change. The Experiment `TASK.md` should record what changed, which checks ran, their results, and what remains unverified.

Distinguish short tests and smoke tests from a full, long-running execution.

## 9. Choosing the execution owner

Choose an execution mode for each Experiment:

| Mode | Meaning |
|---|---|
| `agent` | An authorized agent runs the work and records the result |
| `human` | A human reviews and runs the work |
| `hybrid` | Human and agent divide execution, monitoring, or evaluation |
| `TBD` | The execution owner has not been decided |

Record at least the execution owner in the Experiment `TASK.md`:

```markdown
Execution owner: agent
```

For `hybrid`, specify who does what:

```markdown
Execution owner: hybrid

Agent responsibilities:
- Validate the configuration
- Submit the job and record its ID

Human responsibilities:
- Monitor the long-running job
- Decide how to respond to infrastructure failures
```

If the user explicitly asks an agent to prepare and execute an Experiment, the agent may do both within the authorized scope. Operations requiring additional approval under `AGENTS.md` still require that approval. Approval to create an Experiment is not, by itself, approval to execute it.

## 10. Checks before execution

Whether the owner is an agent or a human, confirm:

- Experiment ID and objective
- Git commit to be executed
- Configuration and variable conditions
- Dataset and checkpoint locations
- Required resources and estimated duration
- Output location
- Resume behavior
- Whether existing results could be overwritten
- Evaluation method
- Any required execution approval

If an unknown condition could change the result, resolve it before starting.

## 11. Execution and monitoring

For `agent` execution, the agent runs the authorized command and records the start time, command, commit, job ID, and output location in `TASK.md`. If the agent's session may end before the job does, leave instructions for monitoring, resuming, and collecting results there.

For `human` execution, `TASK.md` provides a command the human can run directly. The human records the job ID and log location there or provides them to the agent afterward.

For `hybrid` execution, follow the responsibilities documented in `TASK.md`. Both “agent submits, human monitors” and “human runs training, agent evaluates and summarizes” are valid arrangements.

When an execution script is needed, make it runnable from the repository root where practical:

```bash
bash experiments/EXP-xxx_name/run.sh
```

Add `submit.sh` when the environment requires a job scheduler.

## 12. Recording results

Do not normally commit checkpoints or large logs to Git. Record enough execution information in the Experiment `TASK.md` to reproduce and inspect the result:

- Git commit
- Configuration
- Dataset version or split
- Random seed
- Execution environment
- Checkpoint and log locations
- Evaluation command
- Metrics and aggregation method
- Failures or interruptions

The Experiment `README.md` is the source of truth for measured values and their interpretation. In an RQ file, link to the Experiment and describe what its results mean for the hypothesis rather than copying extensive results.

## 13. Interpreting results

Before interpreting a result, review the target RQ, the Experiment's hypothesis and conditions, the recorded results, and related Experiments.

Example prompt for ChatGPT:

> Analyze this Experiment in relation to its RQ. Separate direct observations, supported and weakened hypotheses, claims that cannot yet be made, confounding factors, and candidates for the next Experiment. Present the interpretation for review before modifying files.

After human review, update the Experiment and the relevant RQ. Update the timeline in `research/README.md` only if the overall research direction has changed.

## 14. Interruption and handoff

A person or agent taking over should locate the work in `experiments/README.md` and read the target Experiment's `README.md` and `TASK.md`.

Even when work stops midway, record:

- Current status
- Completed work
- Validation performed and its results
- Active job ID and output location, if applicable
- Known problems and unverified assumptions
- The next concrete action or command
- Branch and commit, when available

The previous chat transcript should not be required to continue.

## 15. Common prompts

### Discuss research without changing files

> Review the target RQ and related Experiments. Help me examine the hypothesis and alternative explanations. Do not modify files yet.

### Turn a discussion into an Experiment proposal

> Turn this discussion into an Experiment proposal following `docs/rex/templates/EXPERIMENT.md` and `docs/rex/templates/TASK.md`. Show me the draft first. Do not save it yet.

### Approve an Experiment

> Create a new Experiment from this approved proposal and add it to `experiments/README.md`. Set the execution owner to `TBD` for now.

### Request implementation

> Read `AGENTS.md` and the target Experiment's `README.md` and `TASK.md`. Implement the documented work and record validation results and remaining tasks in `TASK.md`.

### Ask an agent to execute

> Read the target Experiment's `README.md` and `TASK.md`. Check the configuration and command, then execute within the approved scope. Record the job ID, logs, and status in `TASK.md`, and record measured results in `README.md`.

### Prepare an Experiment for human execution

> Read the target Experiment's `README.md` and `TASK.md`. Prepare it so a human can run it. Record scripts, configuration, pre-run checks, and an exact command in `TASK.md`. Do not launch it.

### Resume interrupted work

> Read `AGENTS.md` and the target Experiment's `README.md` and `TASK.md`. Summarize its current status, remaining work, and next action before continuing.