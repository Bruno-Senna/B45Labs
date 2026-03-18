# B45 Labs Coding Standard (Revit 2023 – 2026)

**Last updated:** 2026-03-18

## 1) Purpose and Scope
- All add-in code must target **Autodesk Revit 2023, 2024, 2025, and 2026** APIs.
- Build targets:
  - **R23 / R24** — `B45Labs_Addin_Legacy` project, `net48`, `REVIT2023` / `REVIT2024` preprocessor symbols.
  - **R25 / R26** — `B45Labs_Addin` project, `net8.0-windows`, `REVIT2025` / `REVIT2026` preprocessor symbols.
- Priority order: **correctness > robustness > maintainability > performance > brevity**.
- The codebase should remain predictable for long-term maintenance and team handoff.

---

## 2) File Organization and Structure
- Every C# file must start with a **standard header** describing:
  - Purpose
  - Key behaviors
  - Revit API notes (cross-version constraints)
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
- Prefer "why" comments over "what" comments.
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
  - `Ensure*` = guarantees a state (e.g., "exists in target")
  - `Build*` / `Create*` = constructs new instances or objects

---

## 5) Revit API Compatibility (2023 – 2026)

### 5.1 ElementId
- **Never use `ElementId.IntegerValue`** (removed in Revit 2025+). Always use:
  - `ElementId.Value` (returns `long`) for numeric IDs and comparisons.
- This applies to all 4 build configurations — use `ElementId.Value` uniformly.

### 5.2 Category comparisons
- Use `category.Id.Value == (long)BuiltInCategory.XXX`

### 5.3 Preprocessor guards
- Use `#if REVIT2025 || REVIT2026` / `#if REVIT2023 || REVIT2024` when APIs diverge.
- Keep guarded blocks small and clearly commented with WHY.

### 5.4 Avoid obsolete APIs
- Document unavoidable exceptions in the file header.

---

## 6) C# Language Version Constraints

### Net48 builds (R23 / R24) — strict subset only
The `net48` (Legacy) project compiles with an older Roslyn toolchain. **Do not use C# 8+ features** in any shared or legacy-targeted file:

| Prohibited in net48 | Alternative |
|---|---|
| `..` range/index operators (`arr[..n]`) | Explicit `Array.Copy` or `Substring` |
| `using var` (implicit dispose scope) | Explicit `using (var x = ...)` |
| `is not null` / `is null` patterns | `!= null` / `== null` |
| Default interface members | Abstract base class |
| Switch expressions | Switch statements |
| Nullable reference types (`string?`) | No annotation; use null checks |
| Records (`record class`) | Regular class with manual equality |

### Net8 builds (R25 / R26)
- C# 12 features are permitted.
- Nullable reference types are encouraged but not required.
- Top-level statements are NOT used (Revit add-ins require explicit class entry points).

---

## 7) Transactions and Document Safety
- Large workflows must be wrapped in a `TransactionGroup`.
- Keep `Transaction`s **small and single-purpose**:
  - "Create Sheet"
  - "Copy Sheet Elements"
  - "Place Viewport"
- Always commit/rollback explicitly:
  - Use `try { Commit() } catch { RollBack() }` for safety.
- Never leave a transaction open across UI interactions.

---

## 8) Error Handling and Best-Effort Behavior
- The command should not fail because **one item** fails.
- Use best-effort patterns:
  - catch exceptions locally, continue processing
  - record "skipped" counters/reasons when relevant
- Avoid silent failures for critical steps:
  - Provide meaningful final reporting (counts + skipped reasons).

---

## 9) Performance (Pragmatic)
- Use `FilteredElementCollector` correctly:
  - restrict by view id when possible
  - filter by class/category early
- Cache expensive lookups when repeated:
  - view name sets
  - preview images
  - type matches
- Avoid repeated full-document scans inside loops.

---

## 10) MVVM and WPF Standards
- ViewModels must be UI-agnostic:
  - no references to Window/UI elements
  - no direct dispatcher logic unless strictly needed
- Use:
  - `INotifyPropertyChanged`
  - `ObservableCollection<T>`
- Bindings should target stable VM properties:
  - `SelectedSheet`, `PreviewImage`, `SummaryText`, etc.
- Prefer `DataTrigger` over converters when possible (especially for visibility/placeholder).
- **`DelegateCommand`** is used outside of `B45Labs.Commands` namespace.
- **`RelayCommand`** is used only inside `B45Labs.Commands`.
- `WindowChrome` + `OnSourceInitialized` is required for every `WindowStyle=None` window.
- **`InfoDialog`** for all user-facing messages — never `TaskDialog`.
- No intro/splash dialogs — context goes in `StatusText`.

---

## 11) Reporting and User Feedback
- Always show a final operation report containing:
  - Created counts
  - Copied counts
  - Placed counts
  - Skipped counts (with reason)
- Reports must be consistent, short, and actionable.
- Result navigable + no issues → activate directly, no InfoDialog.

---

## 12) Code Quality Baselines
- No dead code, no commented-out blocks in production branches.
- Helpers must be reusable and single-responsibility.
- Favor readable code with explicit variable names over micro-optimizations.
- `ElementId.Value` always — never `.IntegerValue`.
- Every `Transaction` opens and closes (commit or rollback) — never leave open.
- All styles declared locally in `Window.Resources` — never reference from another window.

---

## 13) Build Configurations Reference

| Config | Project | Target | Preprocessor |
|---|---|---|---|
| R23 | B45Labs_Addin_Legacy | net48 | REVIT2023 |
| R24 | B45Labs_Addin_Legacy | net48 | REVIT2024 |
| R25 | B45Labs_Addin | net8.0-windows | REVIT2025 |
| R26 | B45Labs_Addin | net8.0-windows | REVIT2026 |

Build order for release: R25 → R26 → R23 → R24. All 4 must be clean before packaging.
