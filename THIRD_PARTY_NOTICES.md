# B45 Labs – Third-Party Notices

**Last updated:** 2026-01-01  
**Applies to:** B45Labs_Addin v1.0.0 (Revit 2025 / 2026 builds)

This document lists third-party components used by the B45 Labs software and the applicable licenses.

---

## 1. Maintenance

Update this file whenever you:

- add, remove, or update NuGet packages or other dependencies;
- start redistributing new runtime components; or
- add/remove third-party assets in the installer.

Recommended workflow:

1. Export a list of NuGet dependencies (and other referenced DLLs you redistribute) for each target build.
2. For each dependency, record at least:
   - component name,
   - version,
   - license type,
   - project URL or vendor,
   - whether the full license text must be shipped.

---

## 2. Third-party components currently redistributed

> Versions below can be filled in from your `csproj` / `packages.lock.json` / NuGet UI.  
> If a component is removed from the installer, remove it from this table as well.

### 2.1 Platform and vendor components

| Component / Package                | Version | License / Terms                | Source / Notes |
|-----------------------------------|--------:|---------------------------------|----------------|
| Autodesk Revit API (RevitAPI.dll, RevitAPIUI.dll, etc.) | 2025 / 2026 | Autodesk EULA | Installed with Autodesk Revit. Referenced only; not redistributed independently. |
| Dynamo Core / Dynamo Services     | (fill)  | Autodesk / Dynamo terms        | Used for Dynamo-related functionality where applicable. |
| Microsoft .NET Runtime Components (System.\*, Microsoft.\*) | (fill) | Microsoft Software License Terms | Installed as part of .NET / Windows. Only standard runtime components are used. |

> Note: B45 Labs does **not** distribute Autodesk or Dynamo binaries outside the standard Revit installation; they are referenced where present on the user’s machine.

### 2.2 Open-source / third-party libraries

These are the main third-party libraries that are actually redistributed with the B45 Labs installer (via NuGet or otherwise):

| Component / Package                | Version | License           | Source / Notes |
|-----------------------------------|--------:|-------------------|----------------|
| ClosedXML                         | (fill)  | MIT               | Excel export / spreadsheet handling. https://github.com/ClosedXML/ClosedXML |
| DocumentFormat.OpenXml           | (fill)  | MIT               | Open XML (XLSX / DOCX) support. https://github.com/OfficeDev/Open-XML-SDK |
| SharpZipLib                       | (fill)  | MIT               | ZIP / compression utilities. https://github.com/icsharpcode/SharpZipLib |
| System.Data.SQLite / SQLite.Interop | (fill) | Public Domain / SQLite License | Local embedded database used for logging and configuration. https://www.sqlite.org |
| Lucene.NET (Core, Analysis.Common, Queries, etc.) | (fill) | Apache 2.0        | Text indexing / search features. https://lucenenet.apache.org |
| IronPython (IronPython, IronPython.Modules, IronPython.SQLite, IronPython.Wpf) | (fill) | Apache 2.0        | Scripting / automation support where enabled. https://ironpython.net |
| Newtonsoft.Json (if present)      | (fill)  | MIT               | JSON serialization. https://www.newtonsoft.com/json |
| Any additional NuGet packages you use (add rows here) | (fill) | (fill)            | e.g. logging, UI helpers, etc. |

If you introduce new NuGet packages or other third-party DLLs in future versions, add them to the table above with their license information.

---

## 3. License texts

Some licenses require that their full text be included with any redistribution (for example, MIT, Apache 2.0, SQLite).  
You can either:

- embed the full license texts directly in this section, **or**
- ship them as separate files (for example under `LICENSES\`) and reference them here.

### 3.1 MIT-licensed components

Components under the MIT license (e.g. ClosedXML, DocumentFormat.OpenXml, Newtonsoft.Json if used) require the MIT license text to be shipped.

> Include the official MIT license text here, or point to a file such as `LICENSES\MIT_ClosedXML.txt`, `LICENSES\MIT_OpenXmlSdk.txt`, etc.

Example reference (no full text):

- ClosedXML – MIT License (see `LICENSES\MIT_ClosedXML.txt`)
- DocumentFormat.OpenXml – MIT License (see `LICENSES\MIT_OpenXmlSdk.txt`)
- Newtonsoft.Json – MIT License (see `LICENSES\MIT_NewtonsoftJson.txt`)

### 3.2 Apache 2.0-licensed components

Components under the Apache License 2.0 (e.g. Lucene.NET, IronPython) require inclusion of the Apache 2.0 license text and, in some cases, NOTICE information.

> Include the official Apache 2.0 license text here, or reference a file such as `LICENSES\Apache-2.0.txt`, plus any specific NOTICE files required by each project.

Example reference:

- Lucene.NET – Apache License 2.0 (see `LICENSES\Apache_LuceneNet.txt`)
- IronPython – Apache License 2.0 (see `LICENSES\Apache_IronPython.txt`)

### 3.3 SQLite

SQLite is generally Public Domain / SQLite License.

Example reference:

- SQLite (System.Data.SQLite / SQLite.Interop) – SQLite License (see `LICENSES\SQLite.txt`)

---

## 4. Questions

For questions about licensing or third-party components in B45 Labs, contact:

- **Vendor:** B45Labs, Inc.  
- **Email:** support@b45labs.com
