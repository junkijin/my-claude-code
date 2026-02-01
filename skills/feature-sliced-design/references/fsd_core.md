# FSD Core Reference (Concise)

## Core Concepts
- **Layers**: Standardized top-level folders that encode responsibility and dependency direction.
- **Slices**: Business/domain groupings inside most layers.
- **Segments**: Technical-purpose groupings inside slices (or directly inside App/Shared).

## Layers (Top → Bottom)
1. `app`
2. `processes` (deprecated)
3. `pages`
4. `widgets`
5. `features`
6. `entities`
7. `shared`

Notes:
- You do **not** need all layers; add only when they add value.
- Do **not** invent new layers; names and semantics are standardized.

## Import Rule (Layer Direction)
- A module in a slice may import only from **lower** layers.
- Slices **cannot** import other slices on the same layer.
- `app` and `shared` are exceptions: no slices, segments can import each other freely.

## Slices
- Define slices by **business/domain meaning**, not by technical type.
- Grouping slices into folders is allowed, but **no code sharing** inside a group folder.
- Avoid “too many features” — only make a feature if it’s reused across pages.

## Segments (Purpose-Based)
Common segment names:
- `ui` — UI components and presentation logic
- `api` — backend interactions and mappers
- `model` — data model, state, business logic
- `lib` — slice-specific utilities
- `config` — feature flags and config

Avoid purpose-agnostic names like `components`, `hooks`, `types`.

## Public API
- Every slice (and segment on slice-less layers) must expose a **public API** (usually `index.ts`).
- External code should import **only** from the public API, not internal files.

Pitfalls:
- **Circular imports** via index files
- **Bundle bloat** if `shared/ui` has one giant index

Mitigations:
- Use per-component indexes in `shared/ui` and `shared/lib`
- Use relative imports within a slice; absolute imports across slices

## Cross-Imports (`@x` notation)
- Use only on **Entities** when real-world relationships require it.
- Example: `entities/user/@x/order` exposes a special API for `entities/order`.
- Keep cross-imports minimal and explicit.

## Tooling (Quick Commands)

**Steiger (architecture linter)**
```bash
npm i -D steiger @feature-sliced/steiger-plugin
npx steiger ./src
```

**ESLint config**
```bash
npm i -D @feature-sliced/eslint-config eslint-plugin-import eslint-plugin-boundaries
# .eslintrc
# { "extends": ["@feature-sliced"] }
```

**CLI generator**
```bash
npm add -g @feature-sliced/cli
fsd entities user --segments ui api
```

## Incremental Migration (Suggested)
1. Normalize `app` and `shared` first.
2. Distribute UI into `pages`/`widgets` (even with violations).
3. Resolve import violations; extract `entities` and `features` gradually.

## Common Pitfalls
- Shared becomes a catch-all dump.
- Too many features → poor discoverability.
- Public API not enforced → deep imports everywhere.
- Tools not integrated into CI → rules erode over time.
