This file defines the shared rules for AI agents working in this repository.

Core principles

* Treat the repository as the primary record of research decisions, work, and results—not as an unquestionable source of truth.
* Treat existing code and documentation as evidence of the current implementation, not proof that the implementation is correct.
* When code, documentation, experiment records, or observed behavior disagree, investigate and report the discrepancy. Do not silently resolve it by assumption.
* Do not rely on chat history as the only record of work or decisions.
* Keep work reproducible and reviewable.
* Leave enough information for another agent or human to continue.
* Do not modify files while the user is still discussing or considering an idea.
* Preserve unrelated user changes.

Required reading

Before non-trivial repository work, read:

1. README.md
2. docs/WORKFLOW.md
3. experiments/README.md
4. The relevant Research Question and Experiment files

When creating an Experiment, also read:

* docs/templates/EXPERIMENT.md

Read only the files relevant to the current request.

Experiment confirmation

Do not automatically create an Experiment.

When the user requests repository work and has not specified how it should be recorded, ask whether to:

* Create a new Experiment
* Add the work to an existing Experiment
* Proceed without an Experiment

Do not create the Experiment or modify repository files until the user answers.

Do not ask this question for:

* Questions and explanations
* Brainstorming or research discussions
* Status checks
* Ideas that the user has not decided to implement

If the user already specified an Experiment or explicitly chose whether to create one, do not ask again.

Recommend an Experiment when the work spans multiple files, requires validation, affects a research conclusion, uses significant resources, or may need to be resumed later.

Creating an Experiment

When the user approves a new Experiment:

1. Determine the next available Experiment ID.
2. Create its directory and README from docs/templates/EXPERIMENT.md.
3. Preserve the original request under User request.
4. Add it to experiments/README.md.
5. Record the work plan before implementation.

Do not require the user to fill in the template.

Use TBD for undecided information and N/A for sections that do not apply. Do not invent objectives, hypotheses, constraints, metrics, or acceptance criteria.

Before making changes

* Inspect the relevant code, configuration, documentation, and tests.
* Check the working tree for existing changes.
* Identify the smallest reasonable change.
* State or record the work plan.
* Define how the change will be validated.
* Ask when missing information would materially change the result.

Do not silently change the objective, constraints, hypothesis, or acceptance criteria.

Implementation rules

* Limit changes to the requested scope.
* Do not delete, overwrite, revert, or reformat unrelated work.
* Avoid unrelated refactoring.
* Follow existing repository conventions.
* Prefer adapters, wrappers, configuration, or inheritance over modifying upstream code.
* Record the reason when third-party or upstream code must be changed.
* Do not hard-code credentials, private data, machine-specific paths, or resource identifiers.
* Keep experiment conditions reproducible through configuration or explicit arguments.

Validation

Run validation appropriate to the change, such as:

* Syntax and import checks
* Configuration loading
* Unit tests
* Regression tests
* Small or reduced-cost smoke tests

Record the executed commands, results, failures, and skipped checks in the relevant Experiment README.

Never report an unexecuted check as successful. If validation cannot be run, state why and provide the exact command a human should execute.

Restricted operations

Do not perform the following without explicit approval:

* Long-running or expensive computation
* Jobs on shared resources
* Large downloads or external uploads
* Paid cloud operations
* Publication or deployment
* Destructive data operations
* Overwriting checkpoints, logs, or results
* Pushing to a remote repository
* Creating or merging pull requests

Approval to create an Experiment is not approval to run an expensive or external operation.

By default, prepare long-running work so a human can review and launch it.

Research records

* Keep research questions, hypotheses, and interpretations under research/.
* Keep work instructions, configurations, execution records, and results under experiments/.
* Link related Research Questions and Experiments.
* Preserve failed and inconclusive work when it provides useful information.
* Update research conclusions only from recorded evidence.

Handoff and completion

At completion or interruption, record:

* Current status
* Work completed
* Major files changed
* Validation performed
* Results and known problems
* Unverified assumptions
* Remaining work
* The next concrete action or command
* Relevant branch and commit, when available

Another person or agent should not need the previous chat to continue.

Mark work as completed only when the acceptance criteria, required validation, and documentation are complete.

If implementation is ready but human execution is still required, mark it as ready rather than completed.

Safety

* Do not commit credentials, private data, personal information, checkpoints, or large generated outputs.
* Do not rewrite Git history or force-push without explicit authorization.
* Respect licenses, access restrictions, and confidentiality requirements.
* Clearly distinguish facts, observations, interpretations, and assumptions.
