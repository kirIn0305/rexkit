# rexkit

A lightweight repository template for research developed by humans and AI agents.

Use it to connect research questions, hypotheses, implementation work, experiments, and results. The repository is a record of decisions and observations—not a guarantee that existing code or documentation is correct.

## Start here

| File | Purpose |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Core instructions for AI agents |
| [WORKFLOW.md](WORKFLOW.md) | How work is proposed, executed, reviewed, and handed off |
| [research/README.md](research/README.md) | Research goals, questions, and overall timeline |
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
│       └── TASK.md
├── research/
│   ├── README.md
│   └── RQ-001_short-name.md
├── experiments/
│   ├── README.md
│   └── EXP-001_short-name/
│       ├── README.md
│       └── TASK.md
└── third_party/
    └── target_repo/              # Git submodule
```

Add directories for original source code, scripts, tests, and outputs only when the project needs them.

## Getting started

1. Create a repository from this template.
2. Add the research code you will build on as a Git submodule under `third_party/`.
3. Describe the research goals and timeline in `research/README.md`.
4. Create a research-question file when a question needs its own hypotheses and history.
5. Document project-specific setup and verification commands once they have been tested.

After cloning a project that uses this template, initialize its submodules:

```sh
git submodule update --init --recursive
```

## Upstream code and extensions

Keep code in `third_party/` unchanged by default. Place new implementations, adapters, configurations, and experiment scripts in this repository.

The parent repository pins each submodule to a specific commit. Update that commit deliberately, and record why it changed and which experiments may be affected.

If work requires modifying upstream code, document the reason in an EXP and decide whether to use an extension point, a maintained fork, or a tracked patch. Do not leave unrecorded changes inside a submodule.

## Research workflow

An EXP is a record for concrete work. It may cover an experiment, environment setup, implementation, investigation, or another task.

Before making repository changes requested in chat, decide whether to create a new EXP, continue an existing EXP, or proceed without one. If the choice is unclear, the agent asks; an EXP is not created automatically. Discussion alone does not require an EXP.

Each EXP identifies who will execute the work: an AI agent, a human, or both. An agent may run authorized work. Work that needs separate execution approval must wait for that approval. If execution is deferred, leave commands, expected outputs, and the current status so someone else can take over.

Record observations and results in the EXP, then update the relevant research question and overall timeline when they change the research direction. See [WORKFLOW.md](WORKFLOW.md) for the detailed process.
