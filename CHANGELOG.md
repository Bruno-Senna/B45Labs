## Changelog
All notable changes to this project will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/) and follows the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) standard.

---

## [2.1.1] – 2026-08-08

> Repairs 2.1.0: PDF export threw on Revit 2023 and 2024, Check Levels reported differences
> that were not there, and renaming a parameter re-filed it under the wrong group on any
> non-English Revit. The parameter group becomes editable, the parameter template arrives
> ready to fill in, and Check Spelling opens in the language you are working in.

### Fixed

- **PDF export on Revit 2023 and 2024 threw on every run.** Check Coordinates, Model Report
  Card and every other PDF output failed with a missing-assembly error. The Autodesk App Store
  security pins moved four bundled Microsoft libraries to a newer major, and .NET Framework
  does not roll forward across one: a Revit 2023 or 2024 session asked for the old identity and
  was refused. Revit 2025 and newer were never affected. The add-in now supplies the matching
  copy itself, for every library in the payload whose requested version differs from the one
  shipped beside it, not only the one that surfaced.
- **Check Levels reported differences that do not exist.** On the Link Comparison tab, levels at
  the same elevation could be flagged ELEV. DIFF while all three columns showed identical values
  and the difference column read 0. Two elevations are now treated as the same level when they
  are within 1/16 in, and a difference too small for the project's units to print is reported in
  inches or millimetres instead of rounding to zero.
- **Renaming a parameter moved it to the wrong group** on Portuguese, Spanish, French and Russian
  installations of Revit. The rename recreates the parameter, and the group it was recreated in
  was resolved from English names only, so every other language fell through to Data.
- **Check Annotations** dropped the duplicate-tag count from its summary line in every language
  except English.
- **Status and state colours now come from the theme palette.** Revit's Light theme no longer
  shows dark-theme colours that were unreadable on a light background, and a selected queued row
  in Check Spaces keeps its selection colour instead of mixing it with the pending-delete tint.
- **Translations caught up.** Seventy-seven strings across Portuguese, Spanish, French and Russian
  had fallen behind and were showing in English, including the whole Parameter Control cleanup and
  merge flow, the Clear View progress messages and the Sheet Navigator docking menu. Every ribbon
  button caption is now translated in all four languages, and the Spanish and Russian tooltips
  stopped referring to the Library by a name retired weeks ago.
- **Check Spelling always opened on English (US)** no matter what language Revit was running in, so
  working in Portuguese meant every note came back flagged. It now opens on the dictionary that
  matches your language, falling back to the same language when your region has no dictionary of its
  own: Revit in Mexican Spanish opens on Spanish, not on English.
- **Check Spelling** right-click menu rendered as a bright system popup in the middle of the dark
  window, and the tick-box column painted a pale box over the selected row.
- **Importing a spreadsheet still open in Excel failed outright** with a file-in-use error, in both
  Parameter Control and Import Parameters from Excel. Writing a sheet and importing it is one task,
  and both now read the file while Excel holds it. The last saved state is what imports.

### Added

- **Parameter Control, Edit** — the Manage tab's Rename / Replace becomes **Edit** and now changes
  the parameter group as well as the name. Leaving the name blank changes only the group, which is
  a single in-place edit: no values are read, rewritten or put at risk.
- **Parameter Control, Change Group** — sets the group on the whole selection at once, for models
  where hundreds of parameters need re-filing. Groups Revit knows but the previous release could
  not offer, among them Visibility, Photometrics and Title Text, are now selectable.

### Changed

- **The parameter template arrives empty and guided.** It no longer ships a sample row, which the
  import read as data if you filled the sheet underneath it, and the six columns with a fixed set of
  valid values now carry drop-downs, so a mistyped data type or group can no longer be accepted
  silently as something else. Columns lead with Parameter Name, matching the grid the template is
  read beside. Files authored with the previous template still import unchanged.
- **Edit opens holding the parameter's current name** instead of an empty box with an instruction to
  leave it blank. Leaving it as it is means no rename, so changing only the group is now the obvious
  path rather than a rule to remember. The details panel above it can be selected and copied.
- **Check Levels: the Spacing field becomes Offset, and it accepts negative values.** The field sets
  where Add and Duplicate place a new level, so it is an offset from an existing level, not a grid
  spacing, and the label now says so. A positive offset places the new level above the highest one;
  a negative offset now builds downward, below the lowest, for basements and site work. Zero stays
  rejected. The suggested default also stopped being a literal conversion: an imperial project now
  proposes 10' instead of 9' 10 1/8", a metric one keeps 3 m.
- **The installer registers as "B45 Labs | Coordination"** in Windows Installed apps, matching the
  other B45 products, so Windows no longer appends "(Current user, 64-bit)" to tell two same-named
  entries apart. Existing installs upgrade in place.

### Platform
- Full support: Revit 2023, 2024, 2025, 2026, and 2027.

---

## [2.1.0] – 2026-08-02

> The suite gets one visual identity, colour analysis in Check Walls, branded Excel and PDF
> reports, contextual F1 help, a Parameter Control that cleans up years of duplicates, and a
> noticeably faster Revit start.

### Added

**Check Walls**
- **Visual Analysis** — paint the walls in your model by Base Level, Wall Type, Workset, Phase
  Created, Phase Demolished, Function, Structural or Problems, with a generated colour palette,
  eight presets, manual colour pinning, a transparency slider, an on-screen legend and a Reset
  that restores the original graphics. Colours show in plans and sections, not only in 3D.
- **Schedule Filters** — the single Level dropdown became seven combinable dimensions, all
  composing with the search box.
- Multi-selecting rows in the grid, or entries in the legend, selects exactly those walls in the
  model and zooms to fit; a new **Isolate Selected Walls** temporarily hides everything else.
- An opt-in **apply as I open views**, so the current colouring follows you instead of needing
  Apply in every view.

**Reports and exports**
- **Branded Excel and PDF** across Check Coordinates, Check Model Health (Overview, Elements,
  Links and Imports, Schedules, Warnings and Size), Check Parameters, Export Worksets, Model
  Progress, Clash Report Converter and Model Report Card. Several of these previously wrote a
  plain text file or nothing at all.
- **User Profile · Export Branding** — set your company name, accent colour and logo once, and
  every generated report carries them.
- **Create Sheets** — the Excel template and the export now share the full branded frame, and the
  export gained the example shared-parameter columns and how-to cell comments that only the blank
  template used to have.

**Check Model Health**
- A **Diagnostics dashboard** with a warnings triage bar splitting warnings into Critical,
  Important, Noise and Uncatalogued, and **Model Size contributor bars** showing what weighs
  around the model (links, images, families).
- **Deep Scan confirmation** — before the family scan runs it tells you how many families it will
  read and how long that should take, estimated from your own previous scans, with a
  don't-ask-again option.

**Parameter Control**
- A new **Cleanup tab** that groups parameters sharing a name, shows what each one actually holds,
  and consolidates them onto a single survivor instead of just deleting the extras. A whole ticked
  batch runs at once, with a tri-state header tick, Shift+click ranges, and a Keep column that
  says why each default survivor was suggested.
- **Merge Selected** on the Manage tab does the same for parameters that do *not* share a name,
  picked straight from the grid.
- A right-click menu on the Manage grid mirroring the toolbar.

**External Tools**
- A shared sliding **Rename panel** in Check Model Version and Upgrade Model Version, with prefix,
  suffix and find-and-replace and a live before/after preview. Applying twice never stacks the
  same suffix.
- Buttons to **add and remove files after the window is open** (Check Model Version had no way at
  all), merging picks across folders and skipping duplicates.
- Upgrade Model Version gained an **overwrite guard**: a per-row warning and a confirmation
  listing every file that would be saved over its own source with no undo.

**Everywhere**
- **Contextual F1 help** — press F1 on a ribbon button, inside an open command window, or on a
  split-button header, and the matching documentation page opens. Windows with no ribbon button of
  their own (results, breakdowns, pickers, sub-dialogs) resolve to their own page.
- **Type-ahead in every list** — click any list or grid and start typing to jump to the match.
- **Completion notifications with counts** — Parameter Control, Smart Purge, Import Worksets,
  Import Parameters from Excel, Create Sheets, Clear View, NWC View and Save Snapshot now say what
  they did instead of finishing silently or dumping a dialog.

**Elsewhere**
- **Check Coordinates** — linked-model cards are collapsible, each a status dot and name that
  expands to the detail, with Expand all / Collapse all.
- **Sync Sheet Issue Date · Stamp mode** — type an issue date and an optional first-issue date and
  write them to their own parameters. Every sheet in the filter is listed, so a first delivery
  with no revisions can still be stamped. A progress bar runs while it writes.
- **Sheet Navigator** — dock the palette to the ViewCube or any corner of the drawing area, a new
  opt-in Home button that zooms to fit (plus Ctrl+Home and Ctrl+Shift+Home), an opacity submenu,
  and it reopens docked next session if you left it open.

### Changed
- **One visual identity across the suite** — the B45 letterhead now heads every command window and
  dialog, the progress popups included, and **"Content Browser" is called "Library"** everywhere
  in the interface, in all five languages.
- **Notifications** — progress and completion share one corner of the monitor running Revit, so an
  operation visibly finishes into its own message. A command never shows both a notification and a
  dialog for one outcome. A run that ends with warnings raises an amber notification that opens
  the full report when clicked.
- **Sliding panels** — one collapsible-panel design across Check Walls, Copy Detail Sheets, Copy
  Entire Sheet, Place on Existing Sheet and Create Sheets, each remembering its state and width
  between sessions.
- **Generated files** — every file the add-in saves defaults to a `B45_` name prefix, so exports
  group together in your Downloads folder. The "Generated with B45 Labs" signature rides on row 1
  of working files you type into, and stays at the bottom of true reports.
- **Parameter Control** — tabs reordered to Manage / Cleanup / Create New / Export; the Manage
  checkbox column is gone in favour of native Ctrl/Shift multi-select; the footer Cancel is gone,
  because every operation commits as it runs; the GUID column is out of the downloadable template;
  Rename runs from a single dialog; and the Excel buttons match Create Sheets in label, order and
  height.
- **Ribbon** — Check + Upgrade Model Version, Check Levels + Check Walls, and Get Element
  Coordinates + Select In-Place Elements became stacked pairs at 24px, matching Autodesk's own
  panel proportions. Several captions were shortened or re-wrapped so they stop pushing the rest
  of the ribbon sideways.
- **Create Sheets** — the import outcome is a structured band with discrete counts and captions,
  warnings tucked behind a collapsible list instead of pushing the grid down the screen.
- **Check Parameters** — the results window pre-selects the first available model, so data appears
  immediately instead of an empty grid.
- **Plug-in Info** — shorter, the redundant text headline replaced by the logo, the content
  scrolls so the footer can never be clipped, and a new section points at the other B45 tools.
- **Translations** — 124 strings that were silently falling back to English are now translated in
  Portuguese, Spanish, French and Russian. The language picker states that the non-English
  languages are beta.
- **Downloads** — the About window's Releases button and the built-in fallback now point at the
  B45 Labs download page.
- **Uninstall** — now also removes the shared program data folder (bundled families, dictionaries)
  once no other B45 product remains installed.
- **Clash Report Converter** — stays Excel-only; the PDF output was dropped.
- **About Me** — the biography was rewritten with the real career narrative, in all languages.

### Fixed
- **Copy Project Parameters** — crashed on every run on Revit 2025 and newer, which made the
  command unusable there.
- **Check Coordinates** — the results window failed to open at all and reported a misleading
  "result window was not found"; it opens again, and a future failure names its real reason.
- **PDF export never worked** — Check Coordinates and Model Report Card always failed with "an
  error occurred while exporting to PDF" because the required fonts were never resolved.
- **Parameter Control** — exporting a project's parameter standard and importing it into the next
  project now actually works: the export wrote column names the importer did not recognise, so the
  file looked re-importable and silently was not, and the shared-parameter identifier now travels
  with it. Consolidating no longer destroys schedule columns. Delete, replace and rename identify
  a parameter by identity instead of by name, so removing the empty duplicate can no longer take
  out the canonical one with all its values. Rename accepts a forward slash again. The header tick
  box is genuinely tri-state. Reading rows on the Cleanup tab no longer enlists them in the next
  batch of deletions.
- **Check Parameters** — re-importing a previously exported report no longer discards every row,
  and no longer fails outright on a non-English interface.
- **Create Sheets** — a blank spreadsheet row no longer imports as a phantom sheet with no number
  and no name; the existing-sheets prompt no longer clips its button captions; and the preview
  grid keeps its selection highlight and B45 styling in both themes.
- **Check Walls** — Reset clears every colour, including paint left behind by an earlier Revit
  session; the phase filters list only phases actually present on walls; generated palette colours
  stay legible on models with many wall types; selecting a legend colour or a grid row no longer
  yanks you out to the 3D view; and the filter dropdowns no longer clip long names.
- **Warnings Breakdown** — selecting several rows now selects them all in the model. A single dead
  element in the snapshot used to kill the entire selection.
- **Check + Upgrade Model Version** — finished rows are readable in the light theme again; Done
  and Failed rows painted as near-black bands that swallowed the destination filename.
- **F1** — pressing it used to open the B45 page *and* Autodesk's Revit help on top of it.
- **Multi-monitor** — notifications, update prompts, announcements and the ribbon dropdowns now
  appear on the monitor running Revit instead of always the primary display, and land correctly on
  desktops that mix display scaling.
- **Light theme** — selected rows washed out in Clash Map, Copy Project Parameters and Create
  Sheets, and several Parameter Control labels were pale blue on white.
- **Dropdowns** — long lists no longer cut off their last item.

### Performance
- **Revit startup** — the usage database no longer initialises on Revit's startup path. It was
  measured at 155-930 ms, between 65% and 88% of the add-in's entire startup cost, and nothing on
  startup needed it.
- **Opening Revit or a model** no longer runs a full census of every element and link in the
  document. It was collected twice per open and never used.
- **Model Size** — repeat Deep Scans are served from the model cache and finish in seconds.

### Security
- Updated the bundled Microsoft runtime libraries to their latest secure versions, following the
  Autodesk App Store security review.

### Platform
- Full support: Revit 2023, 2024, 2025, 2026, and 2027.

## [2.0.3] – 2026-07-20

> A new Model Size tool, a refined interface across the whole suite, and rock-solid
> Copy & Place Detail Sheets on large models.

### Added
- **Model Size** — a new tool that pinpoints what's inflating your model's file size and
  lets you delete unused families in one click, built into a refreshed Check Model Health.

### Changed
- **Interface refresh** — cleaner, more consistent buttons and dialogs across the whole
  suite, tuned for both dark and light themes.
- **Check Spaces** — now modeless: keep working in Revit while the window is open.
- **Create Sheets** — a resizable Target Models panel and a cleaner layout.
- **Place on Existing Sheet** — click anywhere on a preview header to collapse it (not just
  the arrow), plus layout refinements.
- **Parameter Control** — the category picker is now resizable, with a clearer list and a
  "Show only selected" toggle.
- **Sheet Navigator** — smoother fade-in, and it remembers its last position.

### Fixed
- **Copy & Place Detail Sheets** — reliable on large models now: progressive commit, better
  view-tab handling, and no freeze when placing viewports.
- **Light theme** — hard-to-read text and near-invisible button borders fixed across many
  windows (including the Resize Clash Spheres value field).
- **Clear View (Preserve Links)** — correctly restores each link's visibility state.
- **Check Parameters** — the Summary table can be resized by its bottom grip again.
- **Find** — the Find / Previous / Next buttons no longer clip at the window edge.
- **Check Coordinates** — the "unconfigured coordinates" notice no longer needs a scrollbar.

### Platform
- Full support: Revit 2023, 2024, 2025, 2026, and 2027.

---

## [2.0.2] – 2026-07-12

> A polish-and-performance release: an Apple-style toast system that replaces interrupting dialogs, a
> light-theme selection you can actually read, faster startup, and a wave of QA/QC refinements from
> the field.

### Added
- **Apple-style notifications** — routine, non-blocking messages now surface as clean floating toasts
  in the corner of Revit, with a subtle slide-in and auto-dismiss, instead of interrupting your work
  with a dialog.

### Changed
- **Light-theme selection, redesigned** — selected rows now use a clear accent-blue highlight with
  white text, replacing the washed-out look that made values hard to read. Applied consistently across
  ~35 windows, including View, Element, and Warnings Breakdown and Check Parameters results.
- **Parameter Control — rename without losing data** — renaming a parameter now preserves its values
  (including on grouped elements) and keeps it working in schedules and filters. The Rename / Replace
  dialog and its selection now follow your theme correctly.
- **Check Parameters** — Refresh a single tab or everything, an opt-in Select-in-model, Ctrl+Enter
  fill-down, and an in-window Excel import with a simpler, corrected import preview.
- **Check Walls** — grid combo and numeric cells are now fully editable.
- **Faster startup** — the update check no longer blocks the splash path, so Revit reaches a usable
  state sooner, and the critical-update lock is now airtight.
- **Settings, reorganized** — the Visible Modules launcher moved to the end of the Revit Settings panel
  and now reads "Settings," and the plug-in launcher is a clearer two-line "Plug-in / Settings."
- **Window polish** — standardized 32×32 chrome buttons and a unified 1px accent divider across the
  sheet-command windows.

### Fixed
- Light theme: dark text on blue accent buttons (Check Model Health), invisible secondary-button hover
  text (14 windows), and an invisible toast close button (4 toasts).
- The selection checkbox now stays visible on selected rows.
- Corrected stale PayPal references — donations are handled through Stripe.

### Platform
- Full support: Revit 2023, 2024, 2025, 2026, and 2027.

---

## [2.0.1] – 2026-07-10

> A hotfix release polishing the 2.0.0 launch.

### Fixed
- Fixed a Revit crash when editing combo cells in Check Walls.
- Light theme — stronger input and combo borders so controls no longer read as washed out.
- More reliable light/dark theme and language sync across products.
- Installer — self-heal of the legacy add-in manifest, fixing a duplicate add-in ID load error.
- Plugin Info — cleaner version display, plus general stability fixes.

### Platform
- Full support: Revit 2023, 2024, 2025, 2026, and 2027.

---

## [2.0.0] – 2026-07-08

> **B45 Labs is now B45 Labs · Coordination** — and this is the biggest release we've ever shipped.
> A ground-up visual redesign that follows your Revit theme, the whole suite in five languages, a
> wave of new QA/QC tools, a reimagined Create Sheets, and a privacy-first data model. This is the
> release that turns B45 Labs from a toolset into a coordination platform.

This version also marks the start of the **B45 Labs product line**: **Library** (Content Browser,
Family Manager, Detail Library) now ships as its own product, and **Connect** — the in-Revit
assistant — is on the way.

### Added
- **Check Spaces** — a new MEP QA/QC tool for spaces: review Number, Name, Level, offsets, Area, and
  Volume alongside HVAC Zone, Space Type, Occupants, and Design-vs-Calculated heating and cooling
  loads, side by side.
- **Check Areas** — a new modeless editor for areas: edit Number and Name, filter by Area Scheme, see
  Perimeter, and catch Placed / Not Placed / Not Enclosed problems at a glance.
- **Check Annotations** — a new tag-coverage auditor: finds Untagged, Wrong-tag, Empty-tag, Orphan-tag,
  and Duplicate-mark/tag issues across taggable categories, with Active view / All views / Selected
  sheets scopes, an in-model QA status you can approve or ignore (saved with the model), graphic
  highlighting, and reusable presets.
- **Check Monitored Elements** — a new QA/QC command to paint, isolate, and select monitored elements.
- **Sheet & View Navigator** — a new modeless palette to step Previous / Next / Parent Sheet in Project
  Browser order, jump to any sheet, and navigate with Page Up / Page Down on the canvas.
- **Import Parameters from Excel** — a new command that round-trips with Check Parameters: edit in a
  spreadsheet, preview grouped by element, and write values back.
- **Change Language** — a new unified language picker for both the plug-in and Revit, with the ribbon
  updating live (no restart for plug-in-only changes).
- **Multi-language interface** — the plug-in is now available in **English, Português (BR), Español,
  Français, and Русский**. *(The four non-English languages ship as **BETA** — AI-assisted drafts
  pending native review. Tell us where the wording can be better: support@b45labs.com.)*
- **Live theme system** — a two-mode theme (fixed or Follow-Revit) where every window re-tints in real
  time when you switch Revit's light/dark UI. Pick your mode in the Modules dialog.
- **Personalize B45** — a value-first "Personalize B45" panel and a greeting that welcomes you by name
  across the plug-in. Your profile is stored on your PC only and never shared.
- **Broadcast announcements** — an opt-in, signed startup message channel so you hear about new releases
  and news without leaving Revit.
- **Export my data / Erase my data** — full data portability: export everything B45 holds for your
  install, or erase it locally and on our servers, on request.

### Changed
- **Create Sheets — reimagined**: now modeless, builds one sheet list across multiple open models,
  supports Print Sets, sheet-parameter columns, number prefixes/suffixes, "update existing by number,"
  a progress bar, and a redesigned Excel template with date import.
- **Copy to Sheet, Copy Entire Sheet & Place on Existing Sheet — completely revised**: the cross-sheet
  and cross-model documentation workflow was reworked and improved — choose exactly what comes along
  (title blocks, sheet annotations) with tri-state "select all" headers, plus stability and UX polish.
- **Check Parameters — inline editing**: edit instance and type parameter values right in the grid and
  write them back, with locked cells dimmed and empty cells flagged.
- **Warnings Breakdown** — a three-level hierarchy with 3D isolate/highlight, Model vs Documentation
  grouping, refresh, an opt-in "select in model" toggle, and CSV/XLSX export.
- **Import Table by Key** — now imports spreadsheets that don't have an Element ID column.
- **Clear View** — smarter, safer link handling, including a fail-safe "With All Links" mode.
- **Check Rooms** — a scope selector, immediate modeless Apply, and a Name column that no longer repeats
  the room number.
- **"Select in model" is now opt-in** on tools that follow your row selection — browsing a results list
  no longer changes your model selection unless you turn it on.
- **Update notifications are now tiered** — a gentle toast for routine updates, a modal only when it
  matters, replacing the old always-blocking prompt.
- **Visible Modules** — refined, with whole-panel show/hide toggles and correct anchored positioning;
  it's also where you pick the theme mode (fixed or Follow-Revit).
- **Plugin Info (About) — refreshed**: it now lists each installed product's version, follows your Revit
  theme, and lets you opt in to product-news email updates.
- **Ribbon refresh** — a cleaner "Coordination" tab, reorganized panels, icon-only stacked commands, and
  a Help panel that's always visible.
- **Visual consistency pass** — a unified dark dropdown and checkbox everywhere, a reworked scrollbar
  across ~47 windows, consistent 32-px grid rows across the Check family, and a full light-theme
  legibility sweep.
- **Ribbon icons — full redraw**: the entire icon set was reworked from the ground up — crisp light/dark
  glyphs at multiple resolutions (one `.ico` per command with a legacy fallback), with missing and
  mismatched icons reconciled so every command reads as one coherent set across the suite.

### Fixed
- Fixed a crash on Revit shutdown when copying/placing sheets.
- Fixed a freeze-then-crash when changing theme or canvas color.
- Check Coordinates PDF export now works reliably.
- Create Sheets can import an Excel file while the workbook is open.
- Check Model Health reads correctly in non-English Revit and no longer aborts on stale references.
- Correct default 3D view is used in workshared models (Clash Map, Clear Painted).
- Warnings 3D isolate now applies visually.
- Fixed several minor display glitches (stray glyphs in undo names, selection colors).

### Security & Privacy
- **Consent-based, opt-out telemetry**, with your local profile now encrypted at rest (DPAPI) and a path
  sanitizer that strips file paths from diagnostics.
- **Data minimization** — B45 no longer collects operating-system or hardware environment data.
- **Right to erasure** — erase your data locally and request server-side deletion, independent of the
  telemetry setting.
- Hardened the auto-update supply chain: signed manifests with replay protection, and the API secret
  removed from source (injected at build time).
- Foreign add-in crashes are filtered out of our diagnostics — we only log B45's own errors.
- Updated bundled libraries to clear a known security advisory (OpenMcdf → 3.1.4).

### Under the Hood
- Large-model performance: single-pass collectors replace slow O(n²) scans in Check Model Health and
  parameter checking; per-clash isolation in Clash Map.
- Stability: read-only-document guards on every write command, hardened background-event handlers to
  prevent modeless-window crashes, and a sanitizer so raw error text never reaches you.
- Localization infrastructure and Revit-language detection powering the new multi-language UI.
- Full Revit 2027 (.NET 10) compatibility, including database interop and the Check Spaces zone API.

### Just for fun
- 🎮 A couple of easter eggs are hiding in **About Me** to brighten the workday — unlocked by a certain
  legendary button sequence any retro gamer knows by heart. Happy hunting.

### Notes
- Full support: **Revit 2023, 2024, 2025, 2026, and 2027**.
- The four non-English languages ship as **BETA** (AI-assisted drafts). If a translation reads wrong,
  email support@b45labs.com with the command name, the current text, and your suggested wording.
- Feedback and bug reports: [support@b45labs.com](mailto:support@b45labs.com)

---

## [1.2.0] – 2026-05-06

> Content Browser launches, Warnings Breakdown joins Check Model Health,
> a brand-new cross-sheet workflow, and Revit 2027 is now fully supported.

### Added
- **Content Browser** — a new dockable pane to browse, preview, and load
  content directly into the active model. Two sections (your active model
  and your external libraries), each with sub-tabs for:
  - **Families** (loadable `.rfa` from disk and from any open document)
  - **System types** (Walls, Floors, Ceilings, Roofs, Pipes, Ducts, and
    more — apply to selection or import to the active model)
  - **Materials**
  - **Patterns** (drafting and model fill patterns)
  - **Drafting Views** (single-click activate, double-click cross-doc
    insert with auto-rename)

  Includes global search, Favorites and Recents (universal across tabs),
  filter modes (All/Favorites/Recents), thumbnail previews, multiple
  layout/size options, and adaptive layout for narrow dock widths.
- **Place on Existing Sheet** — a new command under *Import from Model*.
  Pick a source model, choose a sheet, pick the views/elements you want,
  and place them on a target sheet in the current model — same position
  or centered, with the source title block brought along.
- **Warnings Breakdown** — Check Model Health now opens a dedicated
  Warnings window with filters, statistics, expandable rows, element-ID
  copy-to-clipboard, and CSV export.
- **Visible Modules** — a new dropdown to show or hide ribbon buttons
  individually (13 modules covered). Changes apply on the fly without
  restarting Revit; a plugin update automatically restores hidden
  buttons so newly added features are discoverable.

### Changed
- **Check Model Health** — threshold colors on the main panel, the
  Warnings card is now a single-click entry into the new Warnings
  Breakdown window, and the rest of the screen gets out of the way
  while you drill in.
- **Model Progress Analyzer** — snapshot timestamps now display in your
  local time (previously UTC), with the offset prefixed (e.g.
  `UTC-04:00`) so the date never feels ambiguous. Comparison view also
  refined for clearer side-by-side reading.
- **Documentation panel** — *Copy Detail Sheets* received a visual
  refresh and a sheet-number fix; *Copy to Sheet* commands consolidated
  into a single, cleaner workflow; *Import from Model* UX cleaned up to
  match the rest of the panel.
- **Upgrade Model Version** — new Settings dialog with per-extension
  destinations and a polished file-source picker; `.rte` templates now
  upgrade through the correct project-document fallback.
- **Sync Sheet Issue Date** — replaced the native message boxes with the
  branded B45 dialog for visual consistency.
- **Localization (groundwork)** — broad refactor that replaces
  name-based Revit lookups with language-independent IDs throughout the
  add-in. Combined with new shared terminology, this is the foundation
  for full multi-language UI support — Portuguese (pt-BR) already
  rendering correctly behind the scenes; the official multi-language
  release lands in the next version.
- **Window centering** — every command window now centers consistently
  over the Revit window, including on multi-monitor setups. The branded
  *InfoDialog* uses the same logic.
- **Stability pass** — across the full add-in: ribbon icon refresh on
  theme change, multi-monitor positioning fixes (Find / Find &
  Replace / Check Spelling), and a long tail of polish across commands.

### Fixed
- **Resize Clash Spheres** — scope-combo regression introduced in v1.1.0
  is resolved.
- **Check Spelling** — v1.1.0 regression resolved; window now opens and
  centers correctly on every monitor configuration.

### Security
- **PdfSharp 6.2.4** — replaced the previous PDF library to drop the
  ImageSharp CVE chain entirely. No paid-license dependency.
- **Update Gate** — HTTPS host allowlist on download URLs and signature
  verification scaffolding for auto-updates.
- **OpenMcdf 2.4.1** — combined with a new RFA input guard, neutralizes
  the GHSA-jxpf-xq2m-q525 advisory at the parser entry point.
- **Telemetry** — error messages are now PII-sanitized before being
  written to the local log. The unobserved-task exception handler now
  ignores exceptions thrown entirely by other Revit add-ins running in
  the same process, eliminating the bulk of cross-add-in noise from the
  error pipeline.

### Notes
- Full support: **Revit 2023, 2024, 2025, 2026, and 2027** (Revit 2027
  promoted from Beta to full support).
- Multi-language UI (Portuguese first, more to follow) ships in the
  next release — the v1.2.0 work is the groundwork that makes it
  possible.
- Feedback and bug reports: [support@b45labs.com](mailto:support@b45labs.com)

---

## [1.1.0] – 2026-05-01

> Check Spelling, Find & Replace, major command rebuilds, and a full platform upgrade.

### Added
- **New Commands (3)**
  - **Check Spelling** — detects spelling errors across text parameters in the model,
    with offline dictionary support (en-US, pt-BR, es-ES) and a custom BIM vocabulary
    filter. Project dictionary supports Export/Import.
  - **Find & Replace** — batch find and replace text across parameters and elements
    throughout the model in a single non-modal operation.
  - **Find** — quick single-term search across model text parameters.
- **Website** — full documentation hub accessible directly from the ribbon. Includes
  command-by-command explanations, short video tutorials, step-by-step guides,
  screenshots, and a user roadmap where users can request features, track
  development, and report issues.
- **Stripe** — support/donation platform upgraded to Stripe for a smoother,
  more reliable experience.
- **Platform — Revit 2027 (Beta)** — experimental support for Revit 2027 via
  `net10.0-windows` build configuration.

### Changed
- **Copy Detail Sheets** — fully rebuilt engine and UX. Faster, more reliable,
  and significantly smoother to use.
- **Create Sheets** — rebuilt from the ground up with a more fluid UX and
  improved error handling throughout.
- **Check Levels, Check Walls, Check Rooms** — UX improvements and expanded
  usage data collection for better analytics.
- **Check Coordinates** — graphical and UX improvements.
- **Parameter Control** — UX refinements.
- **User Profile** — Complete window redesign. New two-column layout with avatar
  card and profile-completion progress. Added *Experience with Revit* selector and
  multi-select discovery tags (with free-text detail for *Other* and
  *Conference / talk*). Legacy saved profiles are migrated automatically.
  Ribbon button label updated to *User Profile*.
- **Sync Sheet Issue Date** — UX improvements.
- **Move Views, Copy View to Sheet, Copy Legends, Copy Schedules** — stability
  improvements across the Documentation panel commands.
- **Documentation panel availability** — *Copy Legends* and *Copy Schedules*
  now require an active sheet (were always enabled); *Create Sheets* and
  *Sync Sheet Issue Date* are now always enabled (previously required an
  active sheet). Behavior now matches what each command actually needs.
- **Check Model Version / Upgrade Model Version** — now accessible without
  an open model.
- **Security** — security improvements across all commands and data collection
  paths; usage and performance telemetry refined and validated.

### Fixed
- PDF, Excel, and other export operations — stability and output corrections.

### Notes
- Full support: **Revit 2023, 2024, 2025, and 2026**.
- Beta support: **Revit 2027**.
- Feedback and bug reports: [support@b45labs.com](mailto:support@b45labs.com)

---

## [1.0.4] – 2026-04-06

> The biggest update yet — 4 new features, a smarter parameter workflow,
> and a full stability pass across the entire add-in.

### Added
- **New Commands (4)**
  - **Parameter Control** — the most requested feature is here. Create, manage, and
    export shared and project parameters without ever leaving Revit. Batch-create
    parameters across multiple categories and groups, inspect everything bound to
    your model, and export to a Revit-ready `.txt` or Excel file in one click.
  - **Model Progress Analyzer** — track your model's evolution over time. Capture
    snapshots of 14+ key metrics and compare them as the project develops. Snapshots
    travel with your `.rvt` file — no external database, no extra steps.
  - **My Profile** — personalize your B45 Labs experience. Set your name, company,
    role, and industry. Your preferred name appears in your greeting every time you
    open the add-in.
  - **Website Button** — quick access to the B45 Labs website directly from the
    ribbon. Release notes, documentation, and roadmap always one click away.

### Changed
- **Check Levels** — more reliable, with improved error handling and edge case coverage.
- **Check Walls** — batch processing stability improvements.
- **Check Parameters** — broader parameter coverage and cleaner error reporting.
- **Code Quality** — general stability pass across all existing commands.
- **Security** — full audit completed. No sensitive data is collected, stored,
  or transmitted.

### Fixed
- **Telemetry** — resolved stability issues in the background data pipeline,
  including session tracking and thread-safety fixes.

### Notes
- Compatible with **Revit 2023, 2024, 2025, and 2026**.
- Feedback and bug reports: [support@b45labs.com](mailto:support@b45labs.com)

---

## [1.0.3] – 2026-03-18 *(Beta)*

### Added

- **New Commands (6)**
  - Check Levels — validates level naming, elevation consistency, and ordering.
  - Check Walls — audits wall types, constraints, and structural parameters.
  - Check Rooms — checks room naming, area, and placement validity.
  - Sync Sheet Issue Date — batch-updates the issue date parameter across sheets.
  - Check Model Version — inspects and reports the Revit version of external files.
  - Upgrade Model Version — batch-upgrades external files to the current Revit version.

- **User Profile**
  - New *My Profile* tab in the About window.
  - Fields: Full Name, Preferred Name, Email, Company, Role, Industry, Sector, How you found us.
  - Preferred Name is used for avatar initials and the greeting message.
  - Profile is saved locally (`%AppData%\B45Labs\user-profile.json`) and synced to Bubble in the background.

- **Platform — Revit 2023 and 2024**
  - Expanded support from Revit 2025/2026 to all four versions: 2023, 2024, 2025, 2026.
  - Unified build system (R23/R24 via `net48` legacy project; R25/R26 via `net8.0-windows`).

### Changed

- **UI — Complete Redesign**
  - All command windows and dialogs rebuilt with the new Autodesk-style visual language.
  - Unified dark theme: consistent colors, spacing, typography, and corner radii throughout.
  - Autodesk brand blue (`#0696D7`) replaces the previous accent (`#2E7CF6`) across all surfaces.
  - Blue divider accent line below every title bar — consistent across all windows.
  - Flat button style (no drop shadows), uniform input field height (`34px`), and tighter spacing.
  - Icons, status bars, toolbar buttons, and DataGrid row styles aligned to the new design system.

- **Code Quality**
  - General stability improvements and internal refactors aligned with B45 coding standards.
  - Improved error handling and best-effort patterns across all commands.
  - `ElementId.Value` used consistently throughout (removed all `.IntegerValue` usages for R25/R26 compatibility).

- **Security**
  - Full security review pass on all commands and telemetry paths.
  - Confirmed: no sensitive data is collected, stored, or transmitted.

### Notes
- This is a **beta release**. Installer distributed as `B45Labs_Installer_v1.0.3_Beta`.
- Compatible with **Revit 2023, 2024, 2025, and 2026**.
- Feedback and bug reports: [support@B45Labs.com](mailto:support@B45Labs.com)

---

## [1.0.2] – 2026-03-01

### Added
- **Documentation Tab (6 new commands)**
  - Move Views
  - Duplicate Views
  - Copy Legends
  - Copy Schedules
  - Create Multiple Sheets
  - Copy Sheet From Another Model
- **UI / About**
  - Updated the About Me content and added an optional donation button.

### Changed
- **UI & Experience**
  - Improved UI consistency across dialogs, icons, and output messages.
  - Rebuilt the About Me experience (layout, content, and behavior).
- **Core Tools**
  - Refactored Check Coordinates for higher reliability and maintainability.
- **Telemetry & Insights**
  - Upgraded usage/error tracking to better understand command distribution and error patterns.
  - Improved mapping consistency for higher reporting quality.
- **Security & Privacy**
  - Completed a code + telemetry security review (no sensitive data is collected).
- **Stability & Maintainability**
  - General stability improvements and internal refactors aligned with B45 coding standards.

### Fixed
- Fixed YouTube link (PT-BR tutorials recorded and currently being published; EN tutorials coming soon).
- Fixed installer issues that could cause installation failures.

### Distribution
- Implemented digital signing for trusted distribution.

---

## [1.0.1] – 2026-01-27

### Changed
- **Legal / Compliance**
  - Updated Terms of Use (EULA) to clarify that B45 Labs is not a technical authority and that all outputs must be independently validated by the user.
  - Updated Privacy Policy wording to clarify telemetry motivations, limitations, and that no sensitive personal data is intentionally collected.
- **Documentation**
  - Updated README telemetry/diagnostics description and references to PRIVACY.md and TERMS.md.
  - Updated SECURITY and SUPPORT references for consistency.

---

## [1.0.0] – 2026-01-01

### Improved
- **Rebrand (BIM Genie → B45 Labs)**
  - Updated naming across UI, ribbon tabs, commands, and documentation.
  - Plugin identity surfaces aligned with the new B45 Labs brand (labels, dialogs, and messaging).
- **Platform & Architecture**
  - Internal refactor to improve stability, maintainability, and long-term scalability.
  - Cleaner separation between UI, core services, and Revit API logic.
- **User Experience**
  - More consistent dialogs, icons, and output formatting across tools.
  - Improved clarity of execution messaging and results for QA/QC review workflows.
- **Reliability & Diagnostics**
  - Best-effort behavior expanded: isolated failures are less likely to break entire operations.
  - Logging and error handling refined for more stable sessions and easier troubleshooting.

### Added
- **New Commands / Toolset Expansion**
  - New commands introduced as part of the ongoing B45 Labs roadmap.
  - Feature coverage expanded across existing tool categories.
- **Compatibility**
  - Added support and validation for Revit 2026 (while maintaining Revit 2025 compatibility).

### Notes
- First stable release, focused on rebranding and platform stabilization.
- Compatible with **Revit 2025** and **Revit 2026**.

---

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
- Visual and rotation adjustments to icons in the "Model Check" tab.
- Fixed bug affecting models with multiple active survey points.

### Notes
- Beta release, compatible with **Revit 2025** only.

---

## [0.0.10-beta] – 2025-07-23

### Added
- Move Views, Toggle Reference Points, Clear View With/Without Links, Reset Chat.
- New icons for all tools, including light/dark variants.
- New command groups in the Ribbon.

### Changed
- Full Ribbon redesign with commands grouped by category.
- Improved dark/light theme detection with dynamic icon switching.

### Fixed
- Command routing inconsistencies due to refactoring.
- Tooltip duplication and icon flickering in light mode.
- Issue where painted elements were not being correctly reset.

### Notes
- Beta release, compatible with **Revit 2025** only.

---

## [0.0.9-beta] – 2025-06-05

### Changed
- Reorganized ribbon commands across appropriate categories.
- Standardized internal command naming for consistency across UI, Assistant, and tracking.

### Fixed
- Button order inconsistencies, tooltip mismatches, and internal mapping issues.

---

## [0.0.8-beta] – 2025-05-30

### Added
- Check Model Health, Check Parameters, Check Painted Elements.
- Export/Import Worksets, Select All In-Place Elements, Clear/Reset Painted Elements.
- External Tools tab (Check Model Version, Upgrade Model Version).
- Change Language, Plug-in Info, YouTube Tutorials.

### Changed
- NWC View, Clash Map, Clear View Preserve Links enhanced.
- Ribbon restructured into consistent user-friendly groups.
- B45 Labs Assistant: dark/light mode, Enter key, Clear Chat button.

### Fixed
- Duplicate `.addin` file creation, JSON serialization issues, visual layout in light theme.

---

## [0.0.7-beta] – 2025-04-12

### Changed
- Clear View command now supports views with View Templates.

### Fixed
- Scroll behavior issue in the B45 Labs Assistant panel.

---

## [0.0.6-beta] – 2025-04-03

### Added
- Analytics: continent, country, city, screen resolution.
- Geolocation API integration.

### Changed
- Assistant personality refined; improved UI/UX interactions.

---

## [0.0.5-beta] – 2025-04-02

### Added
- Bubble sync fully operational.
- "Clear Conversation" button in Assistant.

### Changed
- Clash Map performance improved; Clear View refined.

---

## [0.0.4-beta] – 2025-03-25

### Changed
- Stability, memory, and error handling improvements.
- Unified focus on Revit 2025+ API.

---

## [0.0.3-beta] – 2025-03-23

### Changed
- SQLite database path updated to `C:\ProgramData\B45Labs`.
- Improved version check system and update prompt UX.

---

## [0.0.2-beta] – 2025-03-21

### Changed
- Plugin metadata and text refinements for public testing.

---

## [0.0.1-beta] – 2025-02-20

### Added
- Initial release: core activity tracking, command usage logging, error reporting.
- Local SQLite database and background Bubble sync structure.
