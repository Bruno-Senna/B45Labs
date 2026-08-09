# B45 Labs · Coordination — Revit Add-in

![Revit](https://img.shields.io/badge/Revit-2023--2027-0696D7?style=flat-square&logo=autodesk&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?style=flat-square)
![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)
![Version](https://img.shields.io/badge/Version-2.1.1-0696D7?style=flat-square)
![.NET](https://img.shields.io/badge/.NET-net48%20%2F%208.0%20%2F%2010.0-512BD4?style=flat-square)

> B45 Labs is a productivity-focused Autodesk Revit add-in designed to streamline **coordination**, **auditing**, **documentation**, and **QA/QC** workflows for BIM teams.

> **Brand note:** B45 Labs is now a suite — **Coordination** (this add-in), **Library**, and **Connect**. Previously released as **BIM Genie**.

---

## 💛 Support This Project

B45 Labs is **free to use**. If it saves you time, consider supporting its development:

[![Donate](https://img.shields.io/badge/Donate-PayPal-0070BA?style=for-the-badge&logo=paypal&logoColor=white)](https://www.paypal.com/donate/?business=T99CG72PLZ36U&no_recurring=0&item_name=Donate+to+support+B45+Labs%2C+smart+BIM+tools+for+Revit+to+streamline+documentation+and+QA%2FQC.&currency_code=USD)

Your contributions help keep the project alive and growing. Thank you!

---

## 📸 Overview

![B45 Labs Ribbon](docs/ribbon.png)
*Full ribbon tab — all commands organized by category (QA/QC, Model Management, Utilities, Clash Analysis, Documentation, Analytics, External Tools, Settings).*

![Check Coordinates](docs/checkcoordinates.png)
*Check Coordinates — validates Survey Point, Project Base Point, and Angle to True North across the main model and linked models. Aligned / Not Aligned / Unloaded states are color-coded for quick scanning.*

![Check Model Health](docs/checkmodelhealth.png)
*Check Model Health — full model audit with breakdown by category.*

![Check Spelling](docs/checkspelling.png)
*Check Spelling — offline spell-check across Text Notes, Rooms, Sheets, and View Names. Dictionary support for English, Portuguese, and Spanish with a custom BIM vocabulary filter.*

![Find & Replace](docs/findreplace.png)
*Find & Replace — batch find and replace text across the model with scope controls (Current view / Sheets / Entire project), Sheet Set filtering, case and whole-word options, and a live results grid.*

![Check Levels](docs/checklevels.png)
*Check Levels — validates level naming, elevation consistency, and ordering across the project.*

![Check Rooms](docs/checkrooms.png)
*Check Rooms — room naming, area, and placement validation.*

![Parameter Control](docs/parametercontrol.png)
*Parameter Control — create, manage, and export shared and project parameters across categories without leaving Revit.*

![Create Sheets](docs/createsheets.png)
*Create Sheets — batch sheet creation from a template list.*

![Sync Sheet Issue Date](docs/sheetissuedate.png)
*Sync Sheet Issue Date — batch-update the issue date parameter across sheets based on the latest revision.*

![User Profile](docs/aboutme.png)
*User Profile — personalize your B45 Labs experience with name, role, experience with Revit, and discovery tags.*

---

## ✨ Key Features

### 🔍 QA/QC
- Coordinate validation across main model and linked models
- Model health checks and diagnostics, with a drill-down Warnings Breakdown
- Level, wall, room, space, and area validation
- Tag-coverage auditing (Check Annotations) and monitored-element review
- Parameter and content auditing, with inline parameter editing
- Painted-element detection

### 📄 Documentation
- Check Spelling across Text Notes, Room Names, Sheet Names, and View Names
  (offline dictionaries for English, Portuguese, and Spanish)
- Find and Find & Replace across model text with scope and Sheet Set filters
- Batch view, schedule, legend, and sheet utilities
- Sheet issue date synchronization
- Copy sheets and documentation content from another open model

### ⚙️ Model Management
- Parameter Control — shared and project parameters, batch-create and export
- Check and upgrade external Revit file versions (works even without a model open)
- Export/import worksets
- Select and manage in-place elements

### 🎯 Clash Analysis
- NWC View generation
- Clash Map from Navisworks exports
- Resize Clash Spheres

### 📊 Analytics
- Model Progress Analyzer — capture snapshots of key metrics and track the
  model's evolution over time

### 👤 User Profile
- Name, preferred name, email, company, role, experience with Revit, and how
  you found us (multi-select discovery tags with optional free-text details)
- Avatar and greeting personalized with your preferred name
- Saved locally in `%AppData%\B45Labs\user-profile.json`

---

## 📋 Requirements

| Requirement | Details |
|---|---|
| Autodesk Revit | 2023, 2024, 2025, 2026, 2027 *(full support)* |
| Operating System | Windows |
| .NET | net48 (R23/R24) · net8.0-windows (R25/R26) · net10.0-windows (R27) |
| Admin rights | May be required depending on install location |

---

## 📦 Installation

### Option A — Installer *(recommended)*
1. Download the latest installer from [**Releases**](https://github.com/B45Labs/B45Labs_Coordination/releases).
2. Close Revit before installing.
3. Run the installer and follow the setup wizard.
4. Launch Revit and open the **B45 Labs · Coordination** ribbon tab.

### Option B — Manual
1. Copy the add-in bundle (DLLs + dependencies) to your target directory.
2. Place the `.addin` manifest in the Revit Addins folder.
3. Ensure dependencies are present and unblocked by Windows.

> **Note:**
> Revit 2023 and 2024 use the `net48` build.
> Revit 2025 and 2026 use the `net8.0-windows` build.
> Revit 2027 uses the `net10.0-windows` build.

---

## 🛠️ Commands

### QA/QC
| Command | Description |
|---|---|
| Check Coordinates | Validates Survey Point / Project Base Point / True North across links |
| Check Model Health | Full model health audit with category breakdown |
| Check Levels | Level naming, elevation, and ordering |
| Check Walls | Wall types, constraints, and structural parameters |
| Check Rooms | Room naming, area, and placement |
| Check Spaces | MEP space review — Number, Name, Level, offsets, Area, Volume, and HVAC loads |
| Check Areas | Area editor — Number/Name, Area Scheme filter, Placed / Not Placed / Not Enclosed |
| Check Annotations | Tag-coverage auditor — Untagged, Wrong-tag, Empty-tag, Orphan, and Duplicate |
| Check Monitored Elements | Paint, isolate, and select monitored elements |
| Check Parameters | Parameter auditing with inline value editing, by category |
| Check Painted Elements | Detects painted materials |

### Documentation
| Command | Description |
|---|---|
| Check Spelling | Offline spell-check across text parameters (EN, PT, ES) |
| Find | Quick single-term search across model text |
| Find & Replace | Batch find and replace across parameters and elements |
| Move Elements | Batch move viewports / elements between sheets |
| Duplicate Views | Duplicate views with options |
| Copy Legends | Copy legends across sheets |
| Copy Schedules | Copy schedules across sheets |
| Copy Documentation | Copy sheet + drafting view content from another open model |
| Create Sheets | Reimagined — modeless, multi-model, Print Sets, sheet-parameter columns, Excel import |
| Sheet & View Navigator | Step Previous / Next / Parent sheet; jump to any sheet; Page Up/Down on canvas |
| Import Parameters from Excel | Round-trips Check Parameters values via spreadsheet |
| Sync Sheet Issue Date | Batch-update issue date across sheets |

### Model Management
| Command | Description |
|---|---|
| Parameter Control | Create, manage, and export shared / project parameters |
| Toggle Reference Points | Show/hide Survey, Base, and Internal Origin |
| Get Element Coordinates | Precise element coordinates |
| Select All In-Place Elements | Batch select in-place families |
| Export / Import Worksets | Excel-based workset management |

### Analytics
| Command | Description |
|---|---|
| Model Progress Analyzer | Snapshot-based tracking of model evolution |

### External Tools
| Command | Description |
|---|---|
| Check Model Version | Inspect Revit version of external files *(no model required)* |
| Upgrade Model Version | Batch-upgrade external files *(no model required)* |

---

## 🔄 Updates

B45 Labs includes a built-in update check. When a new version is available, you'll be notified inside Revit.

Download the latest version from [**Releases**](https://github.com/B45Labs/B45Labs_Coordination/releases).

---

## 📊 Telemetry

To improve stability and prioritize development, B45 Labs collects limited, non-sensitive usage signals:
- Commands executed and usage counts
- Error logs and stack traces
- Add-in version, build number, and Revit version
- Approximate region (country/region, derived from IP — IP is not stored)
- Anonymous installation and session identifiers

Optionally, if you fill out the User Profile, we also collect: name, preferred
name, email, company, role, experience with Revit, and how you found us.

No model data, file paths, file contents, geometry, passwords, or device information is collected.
See [PRIVACY.md](PRIVACY.md) for full details.

---

## 📚 Documentation

| Document | Description |
|---|---|
| [TERMS.md](TERMS.md) | Terms of Use / EULA |
| [PRIVACY.md](PRIVACY.md) | Privacy Policy |
| [EULA_B45Labs.md](EULA_B45Labs.md) | Full End User License Agreement |
| [CHANGELOG.md](CHANGELOG.md) | Version history |
| [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) | Open-source licenses |
| [SUPPORT.md](SUPPORT.md) | Support information |
| [SECURITY.md](SECURITY.md) | Security policy |

---

## 🆘 Support

Email: **support@B45Labs.com**

When reporting issues, please include:
- B45 Labs version (e.g., 2.0.0)
- Revit version (2023 / 2024 / 2025 / 2026 / 2027)
- Steps to reproduce
- Screenshot (redact sensitive details)

---

## ©️ Copyright

Copyright (c) 2026 B45 Labs. All rights reserved.
Use of this Software is governed by [TERMS.md](TERMS.md).
