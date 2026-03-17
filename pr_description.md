## Summary

This PR integrates **Spec-Driven Development (SDD)** as a built-in extension in
Gemini CLI. It provides a structured methodology for Context-Driven Development,
inspired by the **Conductor** extension.

## Details

Key changes include:

- **Built-in SDD Extension:** Integrated the core SDD functionality (formerly
  Conductor) as a built-in extension.
- **Command Rebranding:** Renamed all `/conductor:<action>` commands to
  `/spec:<action>` for a cleaner, action-oriented CLI experience.
- **Artifact Storage Migration:** Moved persistent artifacts from `conductor/`
  to `.gemini/specs/` to keep the project root clean.
- **Experimental Guard:** Guarded the entire feature behind the
  `experimental.sdd` feature flag. It must be enabled via `/settings` or
  `settings.json` to be active.
- **Legacy Migration Path:** Added a non-destructive migration prompt for users
  with existing manual Conductor installations, guiding them to uninstall it
  while preserving their project files.
- **Variable Hydration Refactor:** Refactored `FileCommandLoader` to use the
  standardized `hydrateString` utility, automatically enabling support for
  `${workspacePath}`, `${/}`, and other variables in custom commands.
- **Documentation & UI:** Updated README, added a comprehensive SDD user guide,
  and integrated SDD into the documentation sidebar with an experimental badge.
- **Security & Safety:** Updated security policies to allow access to
  `.gemini/specs/` and added a step in setup to ensure these artifacts are
  exempted from `.gitignore`.

Special thanks to **@moisgobg** and **@mahimashanware** for their collaboration
on this feature.

## Related Issues

This PR addresses the following issues:

- Closes #22685 - SDD Phase 2: Migrate to Built-in Commands
- Closes #22690 - SDD: Rename from `/conductor` commands to `/spec` commands
- Closes #22693 - SDD: Migrate from `/conductor` to `.gemini/specs` directory
- Closes #22687 - SDD: Gate specs as an experimental feature
- Closes #22722 - SDD: Add extensionPath logic to unblock style guide, workflow,
  etc artifact retrieval
- Addresses #22692 - SDD: Ship spec-driven development out-of-the-box, as
  designed in Conductor

## How to Validate

1.  Enable the feature flag:
    - Run `/settings`
    - Search for "SDD"
    - Enable **Spec-Driven Development (SDD)**
    - Restart the CLI.
2.  Run `/spec:setup` in a project and follow the interactive guide.
3.  Verify artifacts are created in `.gemini/specs/`.
4.  Run `/spec:create "My feature"` to initialize a new unit of work.
5.  Run `/spec:status` to see progress.
6.  (Legacy users) Install the old Conductor extension manually and verify the
    migration warning appears on startup.

## Pre-Merge Checklist

- [x] Updated relevant documentation and README (if needed)
- [x] Added/updated tests (if needed)
- [x] Noted breaking changes (if any) - _Renamed commands and storage path._
- [x] Validated on required platforms/methods:
  - [x] MacOS
    - [x] npm run
    - [x] npx
