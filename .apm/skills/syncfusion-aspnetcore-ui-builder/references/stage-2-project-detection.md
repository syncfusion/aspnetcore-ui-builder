# Stage 2: Project Detection

**Purpose:** Auto-detect project structure, framework variant, and configuration to ensure generated code integrates seamlessly.

**AI Should Auto-Detect:**

0. **No Project Detection (Fallback)**
   - Scan for: `*.csproj`, `Program.cs`, `Startup.cs`
   - If NO project found:
     1. **Create new ASP.NET Core Razor Pages project** using `dotnet new webapp -n MyRazorApp` command
     2. The project will be created in the current workspace directory
     3. After creation, proceed with detection on the newly created project
     4. All generated code will be placed in the `Pages/` folder of the new project
   - Document: "No existing project detected. Created new ASP.NET Core Razor Pages project."

1. **Framework Type**
   - Scan for: `*.csproj`, `Program.cs`, `Startup.cs`
   - Detect: Razor Pages (most common), MVC
   - Check: Does project have `Pages/` folder? → Razor Pages
   
2. **Razor Pages Specific**
   - Check for: `Pages/_ViewImports.cshtml` → tag helper registration
   - Check for: `Pages/_ViewStart.cshtml` → shared layout
   - Detect: PageModel usage patterns
   
3. **CSS Strategy**
   - Check for: `wwwroot/css/` folder structure
   - Check for: `tailwind.config.js` → Tailwind CSS
   - Check for: `site.css` or `styles.css` → default styling
   - Default: Bootstrap if no CSS framework detected
   
4. **Component/Partial Directory**
   - Common paths: `Pages/Shared/`, `Views/Shared/`, `Components/`
   - Find existing partial views or view components
   
5. **Formatting Rules**
   - Read `.editorconfig` for indent, naming conventions
   - Apply same rules to generated code (typically 4 spaces)
   
6. **Syncfusion License & Package Versioning**
   - Check: Is `SYNCFUSION_LICENSE_KEY` in `appsettings.json` or environment?
   - Prompt: If missing, ask user for license key
   
7. **Syncfusion NuGet Package Version Detection**
   - **Scan `*.csproj` for existing Syncfusion packages:**
     - If `Syncfusion.EJ2.AspNet.Core` exists: Extract existing version
     - Use SAME version for all new Syncfusion packages → Prevents version conflicts
   - **If NO existing Syncfusion packages found:**
     - **Always use the standard installation command:**
     - `dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json`
     - This ensures you always get the most recent stable release from NuGet.org
   - **Document version decision:** Log detected version in stage output
   
**Output:**
Show detected settings:
```
✓ Framework: ASP.NET Core 8.0 Razor Pages
✓ Component Dir: Pages/Shared/
✓ CSS: Tailwind CSS
✓ Tag Helpers: Registered in Pages/_ViewImports.cshtml
✓ Formatting: 4 spaces, VS defaults
✓ Syncfusion Version: [detected version] (detected from csproj)
  OR
✓ Syncfusion Version: * (latest from NuGet.org - no existing packages)
  OR
✓ No existing project detected. Created new ASP.NET Core Razor Pages project.
  → All code will be generated in the Pages/ folder.

```

---

## Build Prevention Checks (MANDATORY)

**Before advancing to Stage 3, AI MUST perform these checks:**

### Check 1: CSS Framework Conflict Detection

```
Scanning CSS strategy...
  ✓ Tailwind CSS detected
  
Checking for conflicting frameworks:
  [ ] Bootstrap CSS in ~/lib/bootstrap/ ?
  [ ] Material CSS in ~/lib/material/ ?
  
Result: ✅ No conflicts found
```

**If conflicts found:**
```
❌ CONFLICT: Multiple CSS frameworks detected
  - Tailwind CSS: ~/css/site.css
  - Bootstrap CSS: ~/lib/bootstrap/dist/css/bootstrap.min.css

ACTION REQUIRED:
  1. Choose ONE framework (recommend Tailwind for Syncfusion)
  2. Remove conflicting framework files
  3. Update _Layout.cshtml to remove conflicting CSS link
  4. Proceed to Stage 3
```

### Check 2: Tag Helper Registration

```
Scanning Pages/_ViewImports.cshtml...
  [ ] Contains @addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
  [ ] Contains @addTagHelper *, Syncfusion.EJ2
  
Result: ✅ Both tag helpers registered
```

**If missing:**
```
❌ MISSING: Syncfusion tag helper not registered

ACTION: Add to Pages/_ViewImports.cshtml:
  @addTagHelper *, Syncfusion.EJ2
```

### Check 3: Layout File Verification

```
Checking Pages/Shared/_Layout.cshtml...
  [ ] Contains Syncfusion CSS link
  [ ] Contains Syncfusion JS link
  [ ] CSS loads BEFORE JS
  [ ] Single CSS framework only
  
Result: ⚠️ Syncfusion resources missing from _Layout.cshtml
```

**If Syncfusion resources missing:**
```
❌ MISSING: _Layout.cshtml does not include Syncfusion theme

ACTION: Update Pages/Shared/_Layout.cshtml:

In <head> section, add:
  <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/bootstrap5.css" />
  <script src="https://cdn.syncfusion.com/ej2/{version}/dist/ej2.min.js"></script>

Before </body> closing tag, add:
  <ejs-scripts></ejs-scripts>

⭐ CRITICAL: <ejs-scripts> REQUIRED for tag helpers to work!

Replace {version} with actual NuGet version (e.g., 24.1.41)
```

### Check 4: NuGet Package Consistency

```
Checking installed packages...
  $ dotnet list package | grep -i syncfusion
  
Syncfusion.EJ2.AspNet.Core              Latest       Latest  ✅
```

**To always get latest published version:**
```
✅ RECOMMENDED: Install without version pinning
  $ dotnet add package Syncfusion.EJ2.AspNet.Core

This automatically installs and updates to the latest stable published release.
No version conflicts. Always current with latest features and bug fixes.
```

**Optional: Pin to specific version if needed:**
```
If you need a specific version for production stability:
  $ dotnet remove package Syncfusion.EJ2.AspNet.Core
  $ dotnet add package Syncfusion.EJ2.AspNet.Core --version 33.2.6

To check current resolved version:
  $ dotnet list package
```

### Check 5: Nullable Reference Type Configuration

```
Checking AdminDashboard.csproj...
  [ ] <Nullable>enable</Nullable> set
  [ ] <ImplicitUsings>enable</ImplicitUsings> set
  
Result: ✅ Strict null checking enabled
```

---

## Prevention Output Summary

After all checks pass, output:

```
✅ BUILD PREVENTION CHECKS PASSED

Summary:
  ✓ Single CSS Framework: Tailwind CSS (no conflicts)
  ✓ Tag Helpers: Registered in _ViewImports.cshtml
  ✓ Layout Resources: Found in _Layout.cshtml
  ✓ Syncfusion Version: Latest Published Release (auto-updated)
  ✓ Null Safety: Enabled in .csproj
  
Ready for Stage 3 ✓
```
