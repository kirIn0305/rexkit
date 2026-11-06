# rexkit

A lightweight repository template for research and tool development by humans and AI agents.

Use it to connect research questions, specifications, implementation work, experiments, and results. The repository is a record of decisions and observations—not a guarantee that existing code or documentation is correct.

## Start here

| File | Purpose |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Core instructions for AI agents |
| [WORKFLOW.md](WORKFLOW.md) | How work is proposed, executed, reviewed, and handed off |
| [specs/README.md](specs/README.md) | Research Questions and tool or feature specifications |
| [experiments/README.md](experiments/README.md) | Queue of planned, ongoing, and completed work |

Templates for individual records are in [templates/](templates/).

## Repository layout

```text
.
├── AGENTS.md
├── README.md
├── docs/
│   ├── WORKFLOW.md
│   └── templates/
│       ├── EXPERIMENT.md
│       ├── RESEARCH_QUESTION.md
│       ├── SPECIFICATION.md
│       └── TASK.md
├── specs/
│   ├── README.md
│   └── RQ-001_short-name.md
├── experiments/
│   ├── README.md
│   └── RQ-001_short-name/
│       └── EXP-001_short-name/
│           ├── README.md
│           └── TASK.md
└── third_party/
    └── target_repo/              # Git submodule
```

Add directories for original source code, scripts, tests, and outputs only when the project needs them.

## Getting started

1. Create a repository from this template.
2. Add the research code you will build on as a Git submodule under `third_party/`.
3. Describe Research Questions and tool or feature specifications in `specs/README.md`.
4. Create an RQ or SPEC file when a question or specification needs its own record.
5. Document project-specific setup and verification commands once they have been tested.

After cloning a project that uses this template, initialize its submodules:

```sh
git submodule update --init --recursive
```

## Upstream code and extensions

Keep code in `third_party/` unchanged by default. Place new implementations, adapters, configurations, and experiment scripts in this repository.

The parent repository pins each submodule to a specific commit. Update that commit deliberately, and record why it changed and which experiments may be affected.

If work requires modifying upstream code, document the reason in an EXP and decide whether to use an extension point, a maintained fork, or a tracked patch. Do not leave unrecorded changes inside a submodule.

## Research and development workflow

An EXP is a record for concrete work. It may cover an experiment, environment setup, implementation, investigation, or another task.

Before making repository changes requested in chat, decide whether to create a new EXP, continue an existing EXP, or proceed without one. If the choice is unclear, the agent asks; an EXP is not created automatically. Discussion alone does not require an EXP.

Each EXP identifies who will execute the work: an AI agent, a human, or both. An agent may run authorized work. Work that needs separate execution approval must wait for that approval. If execution is deferred, leave commands, expected outputs, and the current status so someone else can take over.

Record observations and results in the EXP, then update the relevant RQ or SPEC when they affect its decisions or requirements. See [WORKFLOW.md](WORKFLOW.md) for the detailed process.
