# B45 Labs Coding Standard (Revit 2025/2026)

## 1) Purpose and Scope
- All add-in code must target **Autodesk Revit 2025 and 2026** APIs.
- Priority order: **correctness > robustness > maintainability > performance > brevity**.
- The codebase should remain predictable for long-term maintenance and team handoff.

---

## 2) File Organization and Structure
- Every C# file must start with a **standard header** describing:
  - Purpose
  - Key behaviors
  - Revit API notes (2025/2026 constraints)
  - Design decisions (trade-offs)
- Organize code with clear sections (use `#region` when it improves navigation):
  - Construction / Setup
  - Core Workflow
  - Revit API Helpers
  - UI / MVVM
  - Error Handling / Reporting
  - Cleanup / Disposal

---

## 3) Comments and Documentation (English Only)
- **All comments must be written in English.**
- Prefer “why” comments over “what” comments.
- Add XML docs (`/// <summary>`) for:
  - public classes
  - public methods
  - critical private helpers (anything non-trivial)

---

## 4) Naming Conventions
- Use consistent naming:
  - `PascalCase` for classes, methods, properties
  - `camelCase` for local variables and parameters
  - `_camelCase` for private fields
- Method intent must be explicit:
  - `Try*` = best-effort, should not throw, returns success/failure
  - `Ensure*` = guarantees a state (e.g., “exists in target”)
  - `Build*` / `Create*` = constructs new instances or objects

---

## 5) Revit 2025/2026 API Compatibility
- **Never use `ElementId.IntegerValue`** (removed). Use:
  - `ElementId.Value` (long) for numeric keys/IDs
- When comparing categories:
  - Use `category.Id.Value == (long)BuiltInCategory.XXX`
- Avoid obsolete APIs and document exceptions in the file header if unavoidable.

---

## 6) Transactions and Document Safety
- Large workflows must be wrapped in a `TransactionGroup`.
- Keep `Transaction`s **small and single-purpose**:
  - “Create Sheet”
  - “Copy Sheet Elements”
  - “Place Viewport”
- Always commit/rollback explicitly:
  - Use `try { Commit } catch { RollBack }` for safety
- Never leave a transaction open across UI interactions.

---

## 7) Error Handling and Best-Effort Behavior
- The command should not fail because **one item** fails.
- Use best-effort patterns:
  - catch exceptions locally, continue processing
  - record “skipped” counters/reasons when relevant
- Avoid silent failures for critical steps:
  - Provide meaningful final reporting (counts + skipped reasons).

---

## 8) Performance (Pragmatic)
- Use `FilteredElementCollector` correctly:
  - restrict by view id when possible
  - filter by class/category early
- Cache expensive lookups when repeated:
  - view name sets
  - preview images
  - type matches
- Avoid repeated full-document scans inside loops.

---

## 9) MVVM and WPF Standards
- ViewModels must be UI-agnostic:
  - no references to Window/UI elements
  - no direct dispatcher logic unless strictly needed
- Use:
  - `INotifyPropertyChanged`
  - `ObservableCollection<T>`
- Bindings should target stable VM properties:
  - `SelectedSheet`, `PreviewImage`, `SummaryText`, etc.
- Prefer `DataTrigger` over converters when possible (especially for visibility/placeholder).

---

## 10) Reporting and User Feedback
- Always show a final operation report (e.g., `InfoDialog`) containing:
  - Created counts
  - Copied counts
  - Placed counts
  - Skipped counts (with reason)
- Reports must be consistent, short, and actionable.

---

## 11) Code Quality Baselines
- No dead code, no commented-out blocks in production branches.
- Helpers must be reusable and single-responsibility.
- Favor readable code with explicit variable names over micro-optimizations.

---

## 12) Required Output Style for ChatGPT-Assisted Code
When generating or revising code in this repository:
- Follow this standard exactly.
- Use maximum helpful commentary (English).
- Ensure Revit 2025/2026 compatibility by default.
- Provide drop-in replacement files whenever possible.
