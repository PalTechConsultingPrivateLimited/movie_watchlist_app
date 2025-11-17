<!--
Sync Impact Report

- Version change: 0.1.0 -> 0.2.0
- Modified principles:
	- Simplified: Removed release management and complex versioning guidance
	- Removed: "Contracts & Integration Testing" (moved to optional best practice)
	- Removed: "Observability & Semantic Versioning" (simplified to basic logging)
- Removed sections: Observability & Semantic Versioning, Development Workflow (complex PR requirements)
- Templates updated: `.specify/templates/plan-template.md` ✅ updated
- Templates checked: `.specify/templates/spec-template.md` ✅ no change needed
	`.specify/templates/tasks-template.md` ✅ no change needed
- Follow-ups: none
-->

# Movie Watchlist Constitution

## Core Principles

### Simplicity & Beginner-Friendly
Write code that is easy to understand and maintain. Avoid complex patterns or
over-engineering. Keep projects small and focused on solving one problem well.
Rationale: Makes it easy for beginners to learn and contribute.

### Modular Code
Organize code into small, focused modules with clear purposes. Each module should
do one thing well and be easy to test independently.
Rationale: Keeps code manageable and makes testing straightforward.

### Test-First (Non-Negotiable)
Write tests before implementing features. Tests should verify that code works
correctly and make refactoring safe.
Rationale: Catches bugs early and documents expected behavior.

### Clear Communication
Write clear comments and docstrings. Explain the "why" behind design decisions.
Rationale: Helps beginners understand code and reduces friction when working together.

## Project Scope
This is a small, beginner-friendly project. Technology choices favor simplicity
and clarity (e.g., SQLite for storage, minimal infrastructure). The focus is on
learning and delivering working features, not production-grade reliability.

## Code Contribution Guidelines
- Keep changes small and focused on one feature or fix.
- Write tests for new functionality.
- Add comments explaining non-obvious logic.
- Ensure code passes local tests before submitting changes.

## Governance
This constitution is a living document. Propose changes by discussing them with
the core team. Changes that add or remove principles require team agreement.

**Version**: 0.2.0 | **Ratified**: 2025-11-14 | **Last Amended**: 2025-11-17
