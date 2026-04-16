# Sanitized Project Structure

This tree illustrates architecture organization only. It is not a full source dump.

```text
gains-showcase/
├── README.md
├── LICENSE
├── .gitignore
├── assets/
│   ├── README.md
│   ├── screenshots/
│   │   └── .gitkeep
│   ├── diagrams/
│   │   ├── .gitkeep
│   │   └── system-architecture.mmd
│   └── demo/
│       └── .gitkeep
└── docs/
    ├── architecture.md
    ├── product-decisions.md
    ├── ai-coach-design.md
    ├── backend-overview.md
    ├── future-roadmap.md
    ├── sample-data-models.md
    ├── sample-api-contracts.md
    ├── example-flows.md
    └── sanitized-project-structure.md
```

## Private Production Structure (Conceptual)

```text
GAINS (private app repo)
├── Models/
├── Services/
├── ViewModels/
├── Views/
├── Widgets/
├── functions/
└── Supporting infrastructure/config
```

## Scope Note

- Exact production file names and internal implementation are intentionally omitted.
- This structure exists to communicate module boundaries and system thinking for hiring evaluation.
