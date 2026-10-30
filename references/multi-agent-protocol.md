# Multi-agent investigation protocol

## When parallelism is justified

Use an auxiliary agent only when the task is independent enough that it can be investigated without waiting for another task's result. Good examples:

- Find every writer and reader of a particular state field.
- Trace one named interface from its declarations to callers and implementations.
- Inspect the tests that cover one behavior and identify uncovered edge cases.
- Independently challenge a specific architectural claim with counter-evidence.

Poor examples:

- "Analyze the whole project."
- "Explain the architecture" when the primary agent is doing the same work.
- Running multiple agents with the same broad prompt and comparing their prose.
- Assigning an auxiliary agent a task whose output will only create another unrelated research branch.

## Delegation contract

Every delegated task should include:

1. Parent research question.
2. One bounded sub-question.
3. Relevant paths/symbols or a discovery boundary.
4. Read-only expectation.
5. Expected evidence and report format.
6. Completion criteria.

## Auxiliary-agent prompt

```text
You are a read-only investigation assistant for an existing codebase.

Parent research question:
[State the single main question]

Your one investigation task:
[State one bounded, answerable sub-question]

Scope:
- Inspect only the task and its necessary direct dependencies.
- Provide repository-relative file paths, symbol names, and line numbers when available.
- Distinguish verified facts, inferences, and unknowns.
- Check relevant callers, tests, branches, or counterexamples when useful.
- Do not analyze the entire repository, choose a new research direction, modify source files, or edit shared research notes.
- Do not claim to have run commands or tests unless you actually did so.

Return only:
1. Conclusion
2. Evidence
3. Uncertainty or counter-evidence
4. How the finding affects the parent question
5. One suggested next action for the primary agent
```

## Integration procedure

The primary agent should:

1. Read the report and restate its key claim precisely.
2. Verify the most consequential evidence directly where possible.
3. Compare it against current notes, tests, and other findings.
4. Resolve contradictions by gathering evidence; do not vote among agents.
5. Update the shared notes once, in one place.
6. Record any remaining uncertainty in the question backlog.

## Concurrency and note safety

- Do not allow multiple agents to edit the same notes concurrently by default.
- If two agents work in isolated worktrees, ask them to return reports or patches for review rather than merge notes blindly.
- Avoid launching a third agent unless the second task is also independent and useful.
- If no suitable agent-spawn tool exists, run the auxiliary prompt in a separate session manually.
