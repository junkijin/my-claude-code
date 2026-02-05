# Environment
- macOS. Use macOS-compatible commands (e.g., `cat -e` not `cat -A`).

# Tools
- Use ast-grep skill for structural code search (AST patterns, language constructs). Prefer over text grep.

# Code Style
- Write concise, readable, elegantly structured code. Favor clarity over cleverness.

# Communication
- Be concise. Prefer code examples over abstract explanations.

# Workflow
- In plan mode, write plans in natural language with file paths. Only include code snippets when truly necessary (API signatures, type definitions, complex logic).

# After Code Changes
- Grep for old names/patterns to verify no stale references remain.
- Run type-check to ensure no type errors were introduced.
