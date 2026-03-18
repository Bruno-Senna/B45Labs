# B45 Labs (Revit Add-in)

B45 Labs is a productivity-focused Autodesk Revit add-in designed to streamline **coordination**, **auditing**, and **QA/QC** workflows for BIM teams.

> **Brand note:** This project was previously released under the name **BIM Genie** and has been rebranded to **B45 Labs**.

---

## Key Features

- **Model Check**
  - Coordinate validation and reporting (Survey Point / Base Point / Internal Origin).
  - Model health checks and diagnostics (including links/imports visibility and breakdown).
  - Parameter and content auditing utilities.
  - Level, wall, and room validation.

- **Documentation**
  - Batch documentation tools to speed up common production workflows.
  - View, schedule, legend, and sheet utilities.
  - Sheet issue date synchronization.

- **Model Management**
  - Check and upgrade external Revit file versions.
  - Export/import worksets, select and manage in-place elements.

- **User Experience**
  - Consistent Autodesk-style dark theme across all dialogs.
  - Light/Dark theme-aware icons and UI behavior.
  - User Profile with preferred name, role, industry, and sector.
  - Built-in update check mechanism.

---

## Requirements

- **Autodesk Revit:** 2023, 2024, 2025, or 2026
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

> **Note:** Revit 2023 and 2024 use the `net48` build (`B45Labs_Addin_Legacy`).  
> Revit 2025 and 2026 use the `net8.0-windows` build (`B45Labs_Addin`).

---

## Commands Overview

### QA/QC
- Check Coordinates
- Check Model Health
- Check Levels *(new in v1.0.3)*
- Check Walls *(new in v1.0.3)*
- Check Rooms *(new in v1.0.3)*
- Check Parameters
- Check Painted Elements

### Model Management
- Toggle Reference Points
- Get Element Coordinates
- Select All In-Place Elements
- Clear All Painted Elements
- Export / Import Worksets

### Documentation
- Move Views
- Duplicate Views
- Copy Legends
- Copy Schedules
- Create Sheets
- Copy Sheet From Model
- Sync Sheet Issue Date *(new in v1.0.3)*

### Clash Analysis
- NWC View
- Clash Map
- Resize Clash Spheres

### External Tools
- Check Model Version *(new in v1.0.3)*
- Upgrade Model Version *(new in v1.0.3)*

### Settings
- Change Theme / Language
- Plug-in Info
- YouTube Tutorials

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

No sensitive personal data, file paths, model contents, or geometry is collected.  
See **PRIVACY.md** for full details and limitations.

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
- Revit version (2023 / 2024 / 2025 / 2026),
- steps to reproduce,
- timestamp and screenshot (redact sensitive details).

---

## Copyright

Copyright (c) 2026 B45 Labs.  
All rights reserved.

Use of this Software is governed by the **TERMS.md** agreement.
