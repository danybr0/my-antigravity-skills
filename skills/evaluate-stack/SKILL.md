---
name: evaluate-stack
description: >-
  Critically audits and simplifies any technology stack, framework, or library list proposed by AI agents prior to implementation.
  Enforces a zero-dependency, zero-build bias by replacing heavy third-party packages, bundlers, and abstractions with native platform and browser APIs.
---

# Evaluate Stack: Architecture & Dependency Simplifier

AI coding assistants naturally default to heavy, modern industry boilerplate: bundling React, Tailwind, Vite, TypeScript compilers, and dozens of npm packages for problems that require only a few dozen lines of native code.

Use this skill **prior to the implementation or development phase** (e.g., during or right after `/grill-me`, `/plan`, or architectural brainstorming) to critically audit every proposed dependency and strip the architecture down to its lightest, most maintainable form.

---

## Core Philosophy

1. **Native Platform APIs First**: Modern Web, Node.js, and browser APIs have evolved. `fetch`, `chrome.storage`, `navigator.clipboard`, CSS variables, CSS grid/flexbox, native ES modules, and standard DOM methods make most utility packages obsolete.
2. **Zero-Dependency Bias**: Every dependency is an operational liability, security risk, review delay (e.g., Chrome Web Store / App Store), and maintenance burden. If a native helper under 25 lines can do the job, write the helper.
3. **Zero-Build Preference**: Whenever feasible, favor setups that run directly without a transpilation or bundling step (`pnpm build`, Vite, Webpack). Editing files and refreshing is exponentially faster and less error-prone than debugging bundler configs.
4. **Inspectability & Clarity**: A human or reviewer should be able to audit data flow in under 60 seconds without tracing through multi-layer framework abstractions.

---

## Evaluation Workflow

When this skill is activated (via `/evaluate-stack` or when evaluating an upcoming plan):

### Step 1: Inventory the Proposed Stack
List every proposed:
- Runtime Framework (React, Vue, Svelte, Next.js, etc.)
- Build Tooling & Bundlers (Vite, Webpack, Rollup, PostCSS, Babel)
- Styling Solutions (Tailwind CSS, SCSS, Styled Components)
- Third-Party Libraries (icon libraries, HTTP clients, utility packages, parsers)
- Configuration Files required (`vite.config.ts`, `tailwind.config.js`, `tsconfig.json`, etc.)

### Step 2: The Dependency Stress Test (Component-by-Component)
Audit every component against the 5 Simplification Questions:

| Component Category | Reflexive AI Proposal | The Simplification Challenge | Native / Minimal Alternative |
| :--- | :--- | :--- | :--- |
| **Frontend Framework** | React / Vue / Svelte | Does this app have complex multi-route client state, or is it just tabs, forms, and cards? | **Vanilla DOM / Native Custom Elements / HTML Templates** |
| **Styling** | Tailwind CSS + PostCSS | Does this need a node-based CSS purge/compiler, or can modern CSS handle it? | **Vanilla Modern CSS** (CSS Variables, Flexbox, Grid, native nesting) |
| **Icons** | `lucide-react`, `font-awesome` | Why install a 5 MB package for 4 icons? | **Inline SVGs** or a tiny SVG sprite file |
| **Data Fetching** | `axios`, `request` | Why wrap standard network calls? | Native **`fetch()`** with standard `async/await` |
| **Build & Bundler** | Vite, Rollup, Webpack | Does the target runtime require bundling, or does it natively support ES modules? | **Direct Native Execution** (Zero build step) |
| **State & Storage** | Redux, Zustand, Pinia | Is state simple enough for standard objects and native events? | Simple JavaScript state objects + `localStorage` / `chrome.storage` |

### Step 3: Produce the Stack Audit Report
Present a clear comparison table to the user:

```markdown
### 🔍 Tech Stack Simplification Audit

| Component | Proposed by Agent | Simplified Native Alternative | Decision | Savings |
| :--- | :--- | :--- | :--- | :--- |
| UI Layer | React + ReactDOM | Plain Semantic HTML + Vanilla JS | **Replace** | -140 KB runtime, no vDOM |
| Styling | Tailwind + PostCSS | Modern CSS with Variables | **Replace** | Eliminates PostCSS build step |
| Icons | Lucide React | 4 Inline SVGs | **Replace** | -1 dependency |
| Bundler | Multi-target Vite | Zero build (Native ES modules) | **Eliminate** | Instant dev reload, no dist/ sync |

**Summary Impact:**
- Dependencies: X packages ➔ 0 packages
- Build step: Required ➔ None (Instant refresh)
- Code footprint: ~50 MB (node_modules) ➔ <50 KB clean source
```

### Step 4: Seek User Sign-Off
Ask the user to confirm the simplified stack before any code or scaffolding commands are run:
> *"Would you like to proceed with the simplified, zero-dependency stack, or are there specific frameworks you want to retain?"*
