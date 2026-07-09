# Stage 5: Dependencies Detection

**Purpose:** Detect required NuGet packages, resolve version conflicts, prepare installation commands.

**Note:** This stage PREPARES the installation. Stage 6 will execute the commands automatically (no user action needed).

**AI Should:**

1. **Detect Required Packages:**
   - Scan generated Razor Pages for Syncfusion tag helpers
   - List all required NuGet packages (e.g., `Syncfusion.EJ2.AspNet.Core`)
   - Check for other dependencies

2. **Validate Package Names Against Skills (CRITICAL):**
   - For each mapped component, read the skill's `SKILL.md`
   - Extract the **authoritative package name** from the skill
   - Compare against what the generated code is actually using
   - If mismatch found, use the correct package name from the skill

3. **Check Project's .csproj:**
   - What packages already installed?
   - What versions are currently in use?
   - Any version conflicts?

4. **Resolve Conflicts:**
   - If Syncfusion package already installed:
     - Is version compatible?
     - Suggest upgrade if needed
   - If conflicts exist:
     - Recommend resolution

5. **Prepare Installation Commands:**
   - Generate `dotnet add package` command (Ex: dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json)
   - Always use: `dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json`
   - This ensures latest stable version is always installed from NuGet.org

**Status:** AI detects and prepares commands. Auto-advances to Stage 6 which executes them automatically.

---

## What Happens Next

After Stage 5 (dependencies prepared):
1. **Stage 6:** Agent automatically executes `dotnet add package` commands
2. **Stage 7:** Agent generates Razor Pages, PageModels, and CSS
3. **Stage 8:** Agent performs build verification and validation

**Detailed validation coverage in:** See [stage-8-validation.md](stage-8-validation.md)
