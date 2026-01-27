# B45 Labs (Revit Add-in)

B45 Labs is a productivity-focused Autodesk Revit add-in designed to streamline **coordination**, **auditing**, and **QA/QC** workflows for BIM teams.

> **Brand note:** This project was previously released under the name **BIM Genie** and has been rebranded to **B45 Labs**.

---

## Key Features

- **Model Check**
  - Coordinate validation and reporting (Survey Point / Base Point / Internal Origin).
  - Model health checks and diagnostics (including links/imports visibility and breakdown).
  - Parameter and content auditing utilities.

- **Model Management**
  - Workset export/import workflows (where available).
  - Selection and cleanup utilities to accelerate common BIM tasks.

- **User Experience**
  - Consistent dialogs and outputs for QA review.
  - Light/Dark theme-aware icons and UI behavior.
  - Built-in update check mechanism.

---

## Requirements

- **Autodesk Revit:** 2025 and 2026
- **Operating System:** Windows
- **Installation:** Admin rights may be required depending on install location and machine policy.

---

## Installation

### Option A — Installer (recommended)
1. Download the latest installer from the GitHub **Releases** page.
2. Close Revit before installing.
3. Run the installer and follow the setup wizard.
4. Launch Revit and open the **B45 Labs** ribbon tab.

### Option B — Manual install (advanced)
If you maintain internal deployments:
1. Copy the add-in bundle (DLLs + dependencies) to your target directory.
2. Place the `.addin` manifest in the appropriate Revit Addins folder (per user or all users).
3. Ensure dependencies are present and unblocked by Windows.

---

## Updates

B45 Labs can check for newer versions and prompt you when an update is available.  
The download link points to the GitHub Releases page.

If an update is marked as required for compatibility or stability, some versions may block execution until updated.

---

## Telemetry / Diagnostics (Internal Use)

To improve stability and prioritize development, B45 Labs collects limited usage and diagnostic signals, including:
- commands executed and usage counts,
- error logs,
- model metadata (model name, total element count, total link count),
- approximate region (country/region),
- device/performance signals,
- Revit username.

See **PRIVACY.md** for details and limitations.

---

## Documentation / Legal

- Terms of Use / EULA: **TERMS.md**
- Privacy Policy: **PRIVACY.md**
- Third-Party Notices: **THIRD_PARTY_NOTICES.md**
- Support: **SUPPORT.md**
- Security: **SECURITY.md**

---

## Support

Email: **support@B45Labs.com**

When reporting issues, include:
- B45 Labs version,
- Revit version (2025/2026),
- steps to reproduce,
- timestamp and screenshot (redact sensitive details).

---

## Copyright

Copyright (c) 2026 B45 Labs.  
All rights reserved.

Use of this Software is governed by the **TERMS.md** agreement.

## Telemetry / Diagnostics

To improve stability and prioritize development, B45 Labs collects limited usage and diagnostic signals (non-sensitive), such as:
- commands executed and usage counts,
- error logs,
- model metadata (e.g., model name, total element count, total link count),
- approximate region (country/region),
- device/performance signals,
- Revit username.

See PRIVACY.md for details, purposes, and limitations.
