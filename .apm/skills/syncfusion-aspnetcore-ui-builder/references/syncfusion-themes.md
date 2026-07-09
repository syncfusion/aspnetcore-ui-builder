# Syncfusion Theming Resources for ASP.NET Core

**⚠️ MANDATORY:** After making your framework choice, consult this guide for theme implementation.

## Quick Reference: Syncfusion Themes for ASP.NET Core

| Framework | Syncfusion Theme (Light) | Dark Variant | CSS File Name |
|-----------|------------------|---------|--------------|
| **Tailwind** | Tailwind 3 | Tailwind 3 Dark | `tailwind3.css` / `tailwind3-dark.css` |
| **Bootstrap** | Bootstrap 5 | Bootstrap 5 Dark | `bootstrap5.3.css` / `bootstrap5.3-dark.css` |
| **Material** | Material 3 | Material 3 Dark | `material3.css` / `material3-dark.css` |
| **Fluent** | Fluent 2 | Fluent 2 Dark | `fluent2.css` / `fluent2-dark.css` |

## Theme Registration in ASP.NET Core

### For Razor Pages with Tag Helpers (Recommended)

**Note:** When using Syncfusion tag helpers (`<ejs-grid>`, `<ejs-chart>`, etc.) in Razor Pages. Tag helpers work through the `_ViewImports.cshtml` registration only.

### 1. NuGet Package
Install `Syncfusion.EJ2.AspNet.Core` NuGet package (always get latest version):
```bash
dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json
```

### 3. Theme CSS + Scripts + Script Manager in _Layout.cshtml

Add to `Pages/Shared/_Layout.cshtml`:

**Option A: Bootstrap5 Theme**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - App</title>
    
    <!-- Other CSS frameworks (Bootstrap, etc.) -->
    <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.min.css" />
    <link rel="stylesheet" href="~/css/site.css" asp-append-version="true">
    
    <!-- ⭐ CRITICAL: Syncfusion Theme CSS - Bootstrap5 (load in <head>) -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/bootstrap5.3.css" />
    
    <!-- ⭐ CRITICAL: Syncfusion JavaScript (load in <head>) -->
    <script src="https://cdn.syncfusion.com/ej2/{version}/dist/ej2.min.js"></script>
</head>
<body>
    <header>
        <!-- Navigation -->
    </header>
    
    <!-- Page content -->
    @RenderBody()
    
    <footer>
        <!-- Footer -->
    </footer>
    
    <!-- Your custom scripts -->
    <script src="~/js/site.js" asp-append-version="true"></script>
    
    @await RenderSectionAsync("Scripts", required: false)

    <!-- ⭐ CRITICAL: Syncfusion Script Manager (MUST be present for tag helpers - BEFORE </body>) -->
    <ejs-scripts></ejs-scripts>
</body>
</html>
```

**Option B: Fluent2 Theme**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - App</title>
    
    <!-- Your custom CSS -->
    <link rel="stylesheet" href="~/css/site.css" asp-append-version="true">
    
    <!-- ⭐ CRITICAL: Syncfusion Theme CSS - Fluent2 (load in <head>) -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/fluent2.css" />
    
    <!-- ⭐ CRITICAL: Syncfusion JavaScript (load in <head>) -->
    <script src="https://cdn.syncfusion.com/ej2/{version}/dist/ej2.min.js"></script>
</head>
<body>
    <header>
        <!-- Navigation -->
    </header>
    
    <!-- Page content -->
    @RenderBody()
    
    <footer>
        <!-- Footer -->
    </footer>
    
    <!-- Your custom scripts -->
    <script src="~/js/site.js" asp-append-version="true"></script>
    
    @await RenderSectionAsync("Scripts", required: false)

    <!-- ⭐ CRITICAL: Syncfusion Script Manager (MUST be present for tag helpers - BEFORE </body>) -->
    <ejs-scripts></ejs-scripts>
</body>
</html>
```

**Replace `{latest-version}` with actual version from NuGet (e.g., `33.2.10`)**

**⚠️ CRITICAL REQUIREMENTS:**
- ✅ Theme CSS must load in `<head>` section (BEFORE content) — Choose ONE: Bootstrap5, Fluent2, Material3, or Tailwind3
- ✅ Syncfusion JS must load in `<head>` section (after theme CSS)
- ✅ `<ejs-scripts></ejs-scripts>` tag MUST be present before `</body>` (required for tag helpers)
- ✅ Ordering: Theme CSS → Syncfusion JS (both in `<head>`) → Content → `<ejs-scripts>` (before `</body>`)

## Theme CSS Files (CDN URLs)

Syncfusion themes are loaded via CDN. Use the version matching your installed NuGet package.

**Get Latest Version:**
```bash
dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json
# Then check: dotnet list package | grep -i syncfusion
```

**Current Supported Themes:**

All available Syncfusion ASP.NET Core themes (choose ONE):

| Theme Name | CSS File Name | Notes |
|-----------|-------------|-------|
| **Tailwind 3** | `tailwind3.css` | Modern, minimalist (light) |
| **Tailwind 3 Dark** | `tailwind3-dark.css` | Modern, minimalist (dark) |
| **Bootstrap 5** | `bootstrap5.3.css` | Professional, corporate (light) |
| **Bootstrap 5 Dark** | `bootstrap5.3-dark.css` | Professional, corporate (dark) |
| **Fluent 2** | `fluent2.css` | Microsoft Fluent Design (light) |
| **Fluent 2 Dark** | `fluent2-dark.css` | Microsoft Fluent Design (dark) |
| **Material 3** | `material3.css` | Google Material Design 3 (light) |
| **Material 3 Dark** | `material3-dark.css` | Google Material Design 3 (dark) |

Choose ONE theme CSS (load in `<head>`) and Syncfusion JS (load before `</body>`):

```html
<!-- ⭐ IN <head> section: Choose ONE theme CSS -->

<!-- Tailwind 3 (Light) -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/tailwind3.css" />

<!-- OR Tailwind 3 Dark -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/tailwind3-dark.css" />

<!-- OR Bootstrap 5 (Light) -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/bootstrap5.3.css" />

<!-- OR Bootstrap 5 Dark -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/bootstrap5.3-dark.css" />

<!-- OR Fluent 2 (Light) -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/fluent2.css" />

<!-- OR Fluent 2 Dark -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/fluent2-dark.css" />

<!-- OR Material 3 (Light) -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/material3.css" />

<!-- OR Material 3 Dark -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/material3-dark.css" />
```

```html
<!-- ⭐ BEFORE </body> closing tag: Syncfusion JS (ALWAYS the same) -->
<script src="https://cdn.syncfusion.com/ej2/{version}/dist/ej2.min.js"></script>
<ejs-scripts></ejs-scripts>
```

**Examples:** If NuGet shows version `33.2.10`:

**Bootstrap 5 Light:**
```html
<!-- In <head> section -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.2.10/bootstrap5.3.css" />
<script src="https://cdn.syncfusion.com/ej2/33.2.10/dist/ej2.min.js"></script>

<!-- Before </body> closing tag -->
<ejs-scripts></ejs-scripts>
```

**Tailwind 3 Dark:**
```html
<!-- In <head> section -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.2.10/tailwind3-dark.css" />
<script src="https://cdn.syncfusion.com/ej2/33.2.10/dist/ej2.min.js"></script>

<!-- Before </body> closing tag -->
<ejs-scripts></ejs-scripts>
```

**Fluent 2 Light:**
```html
<!-- In <head> section -->
<link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/33.2.10/fluent2.css" />
<script src="https://cdn.syncfusion.com/ej2/33.2.10/dist/ej2.min.js"></script>

<!-- Before </body> closing tag -->
<ejs-scripts></ejs-scripts>
```
---

**End of Syncfusion Theming Reference**
