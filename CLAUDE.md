# CLAUDE.md

## Session Resume Protocol

Before reading source files or answering project-specific questions, run:

```bash
rtk rag resume
```

If open checkpoints are listed, load the relevant checkpoint and follow its `next_step` before any broad exploration. If no open checkpoint exists, continue with the repository's normal workflow.

## RTK

Prefix shell commands with `rtk` when running from Claude Code.

## RAG-First Protocol

For project-specific architecture, deployment, prior bug, or convention questions, query the appropriate RAG knowledge base before reading source files. If no project-specific RAG result is found, state that clearly before using general knowledge.
