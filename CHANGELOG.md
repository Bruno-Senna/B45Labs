## Changelog
All notable changes to this project will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/) and follows the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) standard.

---

## [1.0.1] – 2026-01-27

### Changed
- **Legal / Compliance**
  - Updated Terms of Use (EULA) to clarify that B45 Labs is not a technical authority and that all outputs must be independently validated by the user.
  - Updated Privacy Policy wording to clarify telemetry motivations, limitations, and that no sensitive personal data is intentionally collected.
- **Documentation**
  - Updated README telemetry/diagnostics description and references to PRIVACY.md and TERMS.md.
  - Updated SECURITY and SUPPORT references for consistency.

## [1.0.0] – 2026-01-01

### Improved
- **Rebrand (BIM Genie → B45 Labs)**
  - Updated naming across UI, ribbon tabs, commands, and documentation.
  - Plugin identity surfaces aligned with the new B45 Labs brand (labels, dialogs, and messaging).

- **Platform & Architecture**
  - Internal refactor to improve stability, maintainability, and long-term scalability.
  - Cleaner separation between UI, core services, and Revit API logic for more predictable behavior.

- **User Experience**
  - More consistent dialogs, icons, and output formatting across tools.
  - Improved clarity of execution messaging and results for QA/QC review workflows.

- **Reliability & Diagnostics**
  - Best-effort behavior expanded: isolated failures are less likely to break entire operations.
  - Logging and error handling refined for more stable sessions and easier troubleshooting.

### Added
- **New Commands / Toolset Expansion**
  - New commands introduced as part of the ongoing B45 Labs roadmap.
  - Feature coverage expanded across existing tool categories to support broader productivity and QA/QC workflows.

- **Compatibility**
  - Added support and validation for Revit 2026 (while maintaining Revit 2025 compatibility).

### Notes
- This is the **first stable release**, focused on rebranding and platform stabilization.
- Compatible with **Revit 2025** and **Revit 2026**.
- Feedback, suggestions, or bug reports: [support@B45Labs.com](mailto:support@B45Labs.com).

------

## [0.0.11-beta] – 2025-08-30

### Improved
- **Get Element Coordinates**
  - Rewritten for higher precision using cross-reference with Spot Elevation.
  - Now automatically detects Survey Point clip status (clipped/unclipped).
  - Fixed X/Y value inversion in specific project contexts.
  - Results are now formatted for better readability (X, Y, Z in clear columns).
  - Organized presentation: Survey Point → Base Point → Internal Origin.

- **Check Coordinates**
  - Now powered by the new `Get Element Coordinates` engine with full precision.
  - Added detection of misalignment between Survey and Base Points.
  - Output messages are clearer and more consistent, with feedback on detected issues.
  - Logic simplified for easier maintenance.

- **Check Model Health**
  - New command: **Links & Imports Breakdown** – analyzes linked RVT and CAD files.
  - Performance optimized in data collection using `FilteredElementCollector`.
  - Better segmentation of internal checks by theme (Overview, Views, Elements, Links...).
  - Outputs are now more user-friendly for reading and auditing.

### Fixed
- Fixed bug where coordinates were mirrored in some models.
- Visual and rotation adjustments to icons in the “Model Check” tab.
- Fixed bug affecting models with multiple active survey points.

### Notes
- This is a **beta release**, currently compatible with **Revit 2025 only**.
- Feedback, suggestions, or bug reports: [support@BIMGenie.com](mailto:support@BIMGenie.com).

---

## [0.0.10-beta] – 2025-07-23

### Added
- **Move Views** – New tool to batch relocate views between sheets.
- **Toggle Reference Points** – Allows quick toggle of Survey Point, Project Base Point, and Internal Origin visibility.
- **Clear View With/Without Links** – New options added to Clear View dropdown.
- **Reset Chat** – New command to reset Assistant history and context.
- **New icons for all tools**, including light/dark variants.
- **New command groups** in the Ribbon: Model Check, Model Management, Clash Analysis, External Tools, and Settings.

### Changed
- Full **Ribbon redesign**:
  - Commands now grouped by category for intuitive access.
  - Icons updated for clarity, visibility, and style.
- Assistant commands were remapped to reflect UI changes.
- Improved dark/light **theme detection** with dynamic icon switching.
- New **icon color palette** based on functional grouping (green = check, red = clash, blue = system, etc.).

### Improved
- B45 Labs Assistant layout and alignment polished.
- Analytics system now accurately tracks usage even with renamed commands.
- Performance improvements in command loading and ribbon rendering.
- Updated installer now fully removes outdated folders and databases.
- Improved icon scaling and crispness on high-DPI displays.

### Fixed
- Fixed command routing inconsistencies due to refactoring.
- Addressed Assistant command mismatch in some Revit versions.
- Resolved tooltip duplication and icon flickering in light mode.
- Fixed issue where painted elements were not being correctly reset.

### Notes
- This is a **beta release**, focused on stability and UI/UX improvements.  
- Compatible only with **Revit 2025**.  
- Feedback and bug reports are welcome at [support@BIMGenie.com](mailto:support@BIMGenie.com).

---

## [0.0.9-beta] – 2025-06-05

### Changed
- Reorganized ribbon commands across their appropriate categories (Model Check, Management, Analysis, etc.)
- Standardized internal command naming for consistency across UI, Assistant, and tracking
- Improved command registration logic and overall structure for better scalability

### Improved
- Assistant interpretation and response mapping updated for renamed and reorganized commands
- Light/Dark theme interface consistency improved
- Minor layout alignment and tooltip standardization

### Fixed
- Button order inconsistencies in some ribbon groups
- Tooltip and label mismatches after ribbon restructuring
- Internal mapping issues between Assistant commands and actual command logic

### Notes
- This is a **beta release** focused on usability and internal command structure refinements  
- Currently supported only for **Revit 2025**  
- Feedback and suggestions: [support@BIMGenie.com](mailto:support@BIMGenie.com).

---

## [0.0.8-beta] – 2025-05-30

### Added

#### Model Check  
- **Check Model Health** – Evaluates overall model integrity.  
- **Check Parameters** – New interactive interface for selecting and analyzing parameters by category.  
- **Check Painted Elements** – Detects and reports painted materials in the model.

#### Model Management  
- **Export Worksets** – Automatically exports worksets to Excel.  
- **Import Worksets** – Allows reimport of worksets with mapping support.  
- **Select All In-Place Elements** – Automatically selects all in-place elements.  
- **Clear Painted Elements** – Removes painted materials from selected elements.  
- **Reset Check Painted Elements** – Resets previously flagged painted elements.

#### External Tools *(new tab created)*  
- Relocated **Check Model Version** and **Upgrade Model Version** into a dedicated tab for external operations.

#### Settings  
- **Change Language** – Switches plugin interface language.  
- **Plug-in Info** – Quick access to version details, author, and support information.

#### Official Tutorials  
- **YouTube Tutorial Videos** – New button linking directly to official B45 Labs YouTube tutorials.

### Changed

- **NWC View** – Enhanced 3D export view generation with adjusted background and standardized view name.  
- **Clash Map** – Improved performance, Excel clash reading, and sphere placement with metadata.  
- **Clear View Preserve Links** – Improved logic to only restore links manually hidden in the current view.  
- **Ribbon Restructure** – Tools reorganized into consistent, user-friendly ribbon groups.  
- **B45 Labs Assistant Improvements**:
  - More fluid and polished UI.  
  - Theme support for both dark and light modes.  
  - Enter key support for message sending.  
  - Clear Chat button added.  
  - Refined assistant personality for a more natural and contextual interaction experience.

### Fixed

- Fixed duplicate `.addin` file creation across multiple folders.  
- Resolved JSON serialization issues affecting Bubble data sync.  
- Corrected visual layout issues in light theme mode.  
- Improved stability when closing Revit automatically through the installer.  
- Fixed assistant misbehavior when reading contextual commands in specific Revit versions.

### Notes

- This is a **beta release**, intended for early testers and internal evaluation.  
- Currently supported only for **Revit 2025**.  
- Feedback and bug reports are welcome at [support@BIMGenie.com](mailto:support@BIMGenie.com).

---

## [0.0.7-beta] – 2025-04-12
### Changed
- Clear View command now supports views with **View Templates**:
  - Detects if a View Template is active and prompts the user with options:
    - Remove the template and apply the Clear View.
    - Proceed without removing the template.
    - Use **Temporary View Properties** mode if available.

### Fixed
- Scroll behavior issue in the **B45 Labs Assistant panel** has been resolved.
  - Users can now smoothly scroll through the chat interface without visual glitches.

---

## [0.0.6-beta] – 2025-04-03
### Added
New fields added to the analytics engine, including continent, country, city, and screen resolution.

Integration with a free geolocation API to collect regional distribution data.

Automatic geolocation and system spec logging for new users.

### Changed
B45 Labs Assistant personality further refined for a more conversational and natural tone.

Improved UI/UX interactions within the Assistant, especially for message handling and flow.

Internal refactor to enhance data serialization and syncing logic.

### Fixed
Better error handling for location-based API failures.

Minor memory usage and stability enhancements during long Revit sessions.

---

## [0.0.5-beta] – 2025-04-02
### Added
- Bubble sync is now fully operational, with stable background data transmission.
- "Clear Conversation" button added to the B45 Labs Assistant panel for better control.

### Changed
- Significant UX improvements to the B45 Labs Assistant, including visual polish, clearer message flow, and enhanced AI personality behavior.
- Clash Map tool performance and responsiveness improved.
- Clear View command refined for more predictable and reliable results.

### Fixed
- General stability improvements and minor internal adjustments.

---

## [0.0.4-beta] – 2025-03-25
### Changed
- Improved plugin stability during startup and execution.
- Optimized memory usage and enhanced error handling.
- Refactored internal processes for better reliability.
- Unified focus on Revit 2025+ to simplify compatibility and support.
- **This plugin was developed using the most advanced and up-to-date features of the Revit 2025+ API to ensure maximum performance, stability, and innovation.**

---

## [0.0.3-beta] – 2025-03-23
### Changed
- Updated SQLite database path to `C:\ProgramData\B45Labs` to ensure data is collected across all user accounts on a machine.
- Improved version check system to block outdated versions of B45 Labs when a new release is available.
- Release date is now correctly formatted and readable (e.g., “March 22, 2025”) instead of showing as a Unix timestamp.
- Enhanced user experience and professionalism in update prompts.

---

## [0.0.2-beta] – 2025-03-21
### Changed
- Updated plugin metadata, including internal name and description adjustments.
- Minor text refinements to prepare for public testing.

---

## [0.0.1-beta] – 2025-02-20
### Added
- Initial release of the B45 Labs Add-in.
- Core functionality for user activity tracking, command usage logging, and error reporting.
- Local SQLite database setup for storing usage data.
- Basic background sync structure prepared for integration with Bubble backend.
