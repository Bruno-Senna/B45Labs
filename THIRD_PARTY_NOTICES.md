# B45 Labs – Third-Party Notices

**Last updated:** 2026-03-01  
**Applies to:** B45Labs_Addin v1.0.2 (Revit 2025 / 2026 builds)

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
3. Ensure any required license texts are shipped with the installer (or embedded below).

---

## 2. Third-party components currently redistributed

> Fill versions below from your `csproj` / `packages.lock.json` / NuGet UI.  
> If a component is removed from the installer, remove it from this table as well.

### 2.1 Platform and vendor components

| Component / Package | Version | License / Terms | Source / Notes |
|---|---:|---|---|
| Autodesk Revit API (RevitAPI.dll, RevitAPIUI.dll, etc.) | 2025 / 2026 | Autodesk EULA | Installed with Autodesk Revit. Referenced only; not redistributed independently. |
| Dynamo Core / Dynamo Services (if used) | (fill) | Autodesk / Dynamo terms | Used for Dynamo-related functionality where applicable. |
| Microsoft .NET Runtime Components (System.\*, Microsoft.\*) | (fill) | Microsoft Software License Terms | Installed as part of .NET / Windows. Only standard runtime components are used. |

> Note: B45 Labs does **not** distribute Autodesk or Dynamo binaries outside the standard Revit installation; they are referenced where present on the user’s machine.

### 2.2 Open-source / third-party libraries

These are the main third-party libraries that are redistributed with the B45 Labs installer (via NuGet or otherwise):

| Component / Package | Version | License | Source / Notes |
|---|---:|---|---|
| BouncyCastle.Cryptography | 2.5.0 | MIT | Cryptography utilities. https://github.com/bcgit/bc-csharp |
| ClosedXML | 0.104.2 | MIT | Excel export / spreadsheet handling. https://github.com/ClosedXML/ClosedXML |
| IronPython | 3.4.2 | Apache 2.0 | Scripting/runtime. https://github.com/IronLanguages/ironpython3 |
| Microsoft.CodeAnalysis.Common | 4.12.0 | MIT | Roslyn compiler platform. Primarily analyzers/dev tooling. https://github.com/dotnet/roslyn |
| Microsoft.CSharp | 4.7.0 | MIT | Microsoft C# runtime helpers. https://github.com/dotnet/runtime |
| Microsoft.IO.RecyclableMemoryStream | 3.0.1 | MIT | Memory stream pooling. https://github.com/microsoft/Microsoft.IO.RecyclableMemoryStream |
| Microsoft.Web.WebView2 | 1.0.2957.106 | MIT | Embedded web UI surface. https://github.com/MicrosoftEdge/WebView2Feedback |
| Microsoft.Win32.Registry.AccessControl | 9.0.2 | MIT | Windows Registry ACL helpers. https://github.com/dotnet/runtime |
| Newtonsoft.Json | 13.0.3 | MIT | JSON serialization. https://www.newtonsoft.com/json |
| PdfSharpCore | 1.3.65 | MIT | PDF generation utilities. https://github.com/ststeiger/PdfSharpCore |
| Revit_AI_Main_Versions_API_x64 | 2025.0.0 | (internal) | Internal package (B45 Labs). Validate distribution scope and licensing internally. |
| System.Data.SQLite | 1.0.119 | Public Domain / SQLite License | SQLite database engine wrapper. https://www.sqlite.org |
| System.Diagnostics.EventLog | 8.0.0 | MIT | Windows Event Log integration. https://github.com/dotnet/runtime |
| System.Diagnostics.PerformanceCounter | 8.0.0 | MIT | Windows performance counters. https://github.com/dotnet/runtime |
| System.Drawing.Common | 8.0.3 | MIT | Drawing primitives. https://github.com/dotnet/runtime |
| System.Management | 9.0.1 | MIT | WMI/management APIs. https://github.com/dotnet/runtime |
| System.Net.Http | 4.3.4 | MIT | HTTP client stack. https://github.com/dotnet/runtime |
| System.Runtime.WindowsRuntime.UI.Xaml | 4.7.0 | MIT | WindowsRuntime/XAML interop helpers. https://github.com/dotnet/runtime |
| System.Security.AccessControl | 6.0.1 | MIT | Access control APIs. https://github.com/dotnet/runtime |
| System.Security.Cryptography.Pkcs | 9.0.2 | MIT | PKCS crypto APIs. https://github.com/dotnet/runtime |
| System.Security.Cryptography.Xml | 9.0.2 | MIT | XML signature APIs. https://github.com/dotnet/runtime |

---

## 3. License texts

Some licenses require that their full text be included with any redistribution (for example, MIT, Apache 2.0, SQLite).  
You can either:
- embed the full license texts directly in this document, **or**
- ship them as separate files (for example under `LICENSES\`) and reference them here.

### 3.1 MIT-licensed components
Components under the MIT license (e.g. ClosedXML, DocumentFormat.OpenXml, Newtonsoft.Json if used) require the MIT license text to be shipped.

Recommended approach:
- Ship: `LICENSES\MIT.txt` (generic MIT text), and optionally keep per-component references if you prefer.

Example references:
- ClosedXML – MIT License (see `LICENSES\MIT.txt`)
- DocumentFormat.OpenXml – MIT License (see `LICENSES\MIT.txt`)
- Newtonsoft.Json – MIT License (see `LICENSES\MIT.txt`)

### 3.2 Apache 2.0-licensed components
Components under the Apache License 2.0 (e.g. Lucene.NET, IronPython) require inclusion of the Apache 2.0 license text and, in some cases, NOTICE information.

Recommended approach:
- Ship: `LICENSES\Apache-2.0.txt`
- Ship any required NOTICE files (if applicable per component).

Example references:
- Lucene.NET – Apache License 2.0 (see `LICENSES\Apache-2.0.txt`)
- IronPython – Apache License 2.0 (see `LICENSES\Apache-2.0.txt`)

### 3.3 SQLite
SQLite is generally Public Domain / SQLite License.

Recommended approach:
- Ship: `LICENSES\SQLite.txt`

Example reference:
- SQLite (System.Data.SQLite / SQLite.Interop) – SQLite License (see `LICENSES\SQLite.txt`)

---

## 4. Questions

For questions about licensing or third-party components in B45 Labs, contact:

- **Vendor:** B45 Labs, Inc.  
- **Email:** support@b45labs.com