# Codebase Understanding Skill

A portable Agent Skill for reading existing codebases, building an evidence-based architecture map, tracing execution flows, maintaining research notes, and coordinating multiple coding agents without losing a single research focus.

## Package contents

```text
codebase-understanding/
├── SKILL.md
├── README.md
├── references/
│   └── multi-agent-protocol.md
└── templates/
    ├── architecture.md
    ├── flow.md
    ├── module.md
    ├── questions.md
    └── session-log.md
```

## Use it

After installing the skill in a supported agent, invoke it explicitly for the most predictable behavior:

- "Use the `codebase-understanding` skill to build a first-pass architecture map of this repository."
- "Use the `codebase-understanding` skill to trace the lifecycle of this request from entry point to result."
- "Use the `codebase-understanding` skill to verify this explanation against the implementation and tests."
- "Use the `codebase-understanding` skill to hand off the current research thread to a second agent."

The skill is designed to work in Chinese or English; it responds in the user's language by default.

## Install across agents

The Agent Skills format uses a folder with a `SKILL.md` manifest and optional supporting files. The **format is portable, but skill discovery paths vary by agent and version**.

### Recommended: project-local installation

Place the whole `codebase-understanding/` folder in a supported project-local skill directory. For Codex, the common repo-local location is:

```text
<repository>/.agents/skills/codebase-understanding/
```

Some clients use a product-specific directory instead. If a client does not discover `.agents/skills/`, copy the entire folder (not just `SKILL.md`) into that client's documented skill directory. Keep this package as the canonical copy, and avoid maintaining divergent versions across clients.

### Personal installation

For a user-level installation, copy the folder into the agent's documented personal skill directory. The exact directory differs by product and may change by version; check that agent's current documentation.

### Shared notes across agents

Keep research notes inside the project working tree (default: `project-notes/`) so every agent working on the same checkout can read them. Do not rely on separate chat histories as the source of truth. If agents use different machines or isolated workspaces, sync the notes through version control or another shared location.

## Safe default

The workflow is read-only toward application source code. It may create or update project research notes when useful, but should inspect existing notes and the worktree first. Auxiliary agents should not concurrently edit the same note files; the primary agent integrates findings.
