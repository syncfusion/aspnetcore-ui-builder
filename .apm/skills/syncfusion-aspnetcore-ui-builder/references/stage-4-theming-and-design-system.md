# Stage 4: Theme Selection (Simplified)

**Purpose:** Select a Syncfusion theme for clean, professional UI rendering.

## Overview

This stage is straightforward:

- **Pick a Syncfusion theme** (Bootstrap 5, Tailwind 3, Material 3, or Fluent 2)
- **Ensure clean layout** with Syncfusion CSS properly registered
- **Minimal custom CSS** only if needed for minor tweaks
- **Dark mode:** Not applied unless explicitly requested by customer (avoid custom dark CSS without request)

**Output:** Theme selected and ready for code generation in Stage 5.

---

## Theme Options

Choose ONE Syncfusion theme (light mode) for your entire application:

| Theme | Style Sheet | Best For | Notes |
|-------|------------|----------|-------|
| **Bootstrap 5** | `bootstrap5.3.css` | Professional, corporate UIs | Clean, predictable, widely used |
| **Tailwind 3** | `tailwind3.css` | Modern, minimalist UIs | Lightweight, contemporary feel |
| **Material 3** | `material3.css` | Google Material Design | Polished, system-oriented |
| **Fluent 2** | `fluent2.css` | Microsoft-style UIs | Smooth, adaptive design |

**Dark Mode:** Available if needed (see dark theme variants at bottom of this page)

## How to Choose

- **No strong preference?** → Use **Bootstrap 5** (`bootstrap5.3.css`)
- **Want modern, minimal?** → Use **Tailwind 3** (`tailwind3.css`)
- **Want Google Material look?** → Use **Material 3** (`material3.css`)
- **Want Microsoft Fluent design?** → Use **Fluent 2** (`fluent2.css`)

**Output:** Theme selected

---

## Theme Registration Checklist

After selecting a theme, Agent will:

1. ✅ Verify `_ViewImports.cshtml` has tag helper registration
2. ✅ Update `Pages/Shared/_Layout.cshtml` with theme CSS and scripts
3. ✅ Add `<ejs-scripts></ejs-scripts>` (CRITICAL for tag helpers)
4. ✅ Verify Syncfusion NuGet package is installed

### Required _Layout.cshtml Updates

The layout file MUST include:

```html
<head>
    <!-- ⭐ Theme CSS (in <head>) - Pick ONE based on stage 4 selection -->
    
    <!-- EXAMPLE: Bootstrap 5 (Recommended) -->
    <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/bootstrap5.3.css" />
    
    <!-- EXAMPLE: Tailwind 3 -->
    <!-- <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/tailwind3.css" /> -->
    
    <!-- EXAMPLE: Material 3 -->
    <!-- <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/material3.css" /> -->
    
    <!-- EXAMPLE: Fluent 2 -->
    <!-- <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/fluent2.css" /> -->
    
    <!-- Note: Dark theme variants available upon request (tailwind3-dark, bootstrap5.3-dark, material3-dark, fluent2-dark) -->
    
    <!-- ⭐ Syncfusion JS (in <head>) -->
    <script src="https://cdn.syncfusion.com/ej2/{version}/dist/ej2.min.js"></script>
</head>
<body>
    <!-- Page content renders here -->
    @RenderBody()
    
    <!-- ⭐ CRITICAL: Script Manager (before </body>) -->
    <ejs-scripts></ejs-scripts>
</body>
```

**Replace `{version}` with your NuGet version (e.g., `24.1.41`)**

**Theme CSS File Names:**
- **Bootstrap 5:** `bootstrap5.3.css` (light) or `bootstrap5.3-dark.css` (dark)
- **Tailwind 3:** `tailwind3.css` (light) or `tailwind3-dark.css` (dark)
- **Material 3:** `material3.css` (light) or `material3-dark.css` (dark)
- **Fluent 2:** `fluent2.css` (light) or `fluent2-dark.css` (dark)

**⚠️ CRITICAL ORDERING:**
1. Theme CSS in `<head>` (first)
2. Syncfusion JS in `<head>` (after theme CSS)
3. Content renders
4. `<ejs-scripts></ejs-scripts>` before `</body>` closing tag

---

## Stage 4 Decision Checklist

Upon completion, confirm:

- ✅ Theme selected from:
  - **Bootstrap 5** (`bootstrap5.3.css`) — Recommended
  - **Tailwind 3** (`tailwind3.css`)
  - **Material 3** (`material3.css`)
  - **Fluent 2** (`fluent2.css`)
- ✅ CSS file name documented
- ✅ **Dark mode variant requested by customer?** 
  - If NO → Use light theme only
  - If YES → Use `{theme}-dark.css` instead
- ✅ **Custom CSS dark mode overrides?**
  - Do NOT create unless explicitly requested
- ✅ Ready to proceed to Stage 5

That's it. Simple and clean.
