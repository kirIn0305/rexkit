# rexkit

A lightweight repository template for research and tool development by humans and AI agents.

Use it to connect research questions, specifications, implementation work, experiments, and results. The repository is a record of decisions and observations—not a guarantee that existing code or documentation is correct.

## Start here

| File | Purpose |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Core instructions for AI agents |
| [docs/rex/WORKFLOW.md](docs/rex/WORKFLOW.md) | How work is proposed, executed, reviewed, and handed off |
| [specs/README.md](specs/README.md) | Research Questions and tool or feature specifications |
| [experiments/README.md](experiments/README.md) | Queue of planned, ongoing, and completed work |

Templates for individual records are in [docs/rex/templates/](docs/rex/templates/).

## Repository layout

```text
.
├── AGENTS.md
├── README.md
├── docs/
│   └── rex/
│       ├── README.md
│       ├── WORKFLOW.md
│       └── templates/
│           ├── EXPERIMENT.md
│           ├── RESEARCH_QUESTION.md
│           ├── SPECIFICATION.md
│           └── TASK.md
├── specs/
│   ├── README.md
│   └── RQ-001_short-name.md
├── experiments/
│   ├── README.md
│   └── RQ-001_short-name/
│       └── EXP-001_short-name/
│           ├── README.md
│           └── TASK.md
├── third_party/
│   └── reference_repo/           # Unmodified Git submodule
└── workspaces/
    └── development_repo/         # Independent, editable Git repository
```

Add directories for original source code, scripts, tests, and outputs only when the project needs them.

## Getting started

1. Create a repository from this template.
2. Add repositories that will remain unchanged as Git submodules under `third_party/`.
3. Clone repositories that you will modify and commit to under `workspaces/`.
4. Describe Research Questions and tool or feature specifications in `specs/README.md`.
5. Create an RQ or SPEC file when a question or specification needs its own record.
6. Document project-specific setup and verification commands once they have been tested.

After cloning a project that uses this template, initialize its submodules:

```sh
git submodule update --init --recursive
```

## External repositories

Use `third_party/` for repositories that are only referenced or executed. Keep these repositories unchanged. The parent repository tracks them as Git submodules and pins each one to a specific commit.

Use `workspaces/` for repositories whose code will be modified. Add each repository as a Git submodule. Each repository under `workspaces/` is an independent Git repository: create branches and commits there, not in the rexkit repository.

Record the source URL and commit SHA used by an Experiment. Update a `third_party/` submodule commit deliberately, and record why it changed and which Experiments may be affected. Do not leave unrecorded changes inside a submodule; move editable work to `workspaces/` instead.

Place implementations owned by the rexkit project, adapters, configurations, and experiment scripts directly in this repository when they do not belong to an external repository.

## Research and development workflow

An EXP is a record for concrete work. It may cover an experiment, environment setup, implementation, investigation, or another task.

Write documents under `specs/` and `experiments/` in Japanese. Keep code, commands, paths, identifiers, proper nouns, and quoted source text in their original form when appropriate.

Before making repository changes requested in chat, decide whether to create a new EXP, continue an existing EXP, or proceed without one. If the choice is unclear, the agent asks; an EXP is not created automatically. Discussion alone does not require an EXP.

Each EXP identifies who will execute the work: an AI agent, a human, or both. An agent may run authorized work. Work that needs separate execution approval must wait for that approval. If execution is deferred, leave commands, expected outputs, and the current status so someone else can take over.

Record observations and results in the EXP, then update the relevant RQ or SPEC when they affect its decisions or requirements. See [docs/rex/WORKFLOW.md](docs/rex/WORKFLOW.md) for the detailed process.
