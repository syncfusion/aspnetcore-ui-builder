# Stage 6: Install Dependencies (Automated)

**Purpose:** Automatically execute package installation commands. NO user action required.

**Prerequisites:**
- Stage 5 completed (dependencies detected and installation commands generated)
- Agent has access to terminal/PowerShell in project root directory
- Internet connectivity available for NuGet package download

---

## Installation Process (Automated by Agent)

### Step 1: Agent Navigates to Project Directory

The agent automatically changes to the project root directory where `.csproj` file exists.

### Step 2: Agent Executes Installation Commands

Agent runs the installation command automatically:
```bash
dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json
```

**Expected Output:**
```
info : PackageReference for package 'Syncfusion.EJ2.AspNet.Core' version '(latest)' 
       added to file 'YourProject.csproj'.
```

### Step 3: Agent Verifies Installation

Agent automatically verifies the package was installed:
```bash
dotnet list package | grep -i syncfusion
```

**Expected Output:**
```
Syncfusion.EJ2.AspNet.Core    [latest installed version]
```

### Step 4: Agent Restores Dependencies

Agent automatically restores all dependencies:
```bash
dotnet restore
```

### Step 5: Agent Reports Status

Agent displays installation status:
- ✅ Success: "Packages installed successfully. Ready for Stage 7."
- ❌ Error: Reports specific error with troubleshooting guidance

---

## Troubleshooting (Agent Handles Automatically)

### Issue: "Unable to resolve package"

**Agent Action:**
- Verifies internet connection
- Checks NuGet source is accessible: `https://api.nuget.org/v3/index.json`
- Retries installation up to 3 times with exponential backoff
- If still fails → Report error to user with network troubleshooting guidance

### Issue: "Package already exists"

**Agent Action:**
- Detects package is already installed
- Continues to Stage 7 (no action needed)
- Reports: "Package already installed. Proceeding to code generation."

### Issue: "Access denied" or "Permission denied"

**Agent Action:**
- Attempts installation with current permissions
- If fails → Reports error asking user to:
  - (Windows) Run terminal as Administrator
  - (macOS/Linux) Check directory permissions
  - Wait for user confirmation before retrying

### Issue: ".NET version compatibility"

**Agent Action:**
- Verifies .NET version: `dotnet --version`
- If < 8.0 → Reports error: "Requires .NET 8.0 or higher"
- Waits for user to upgrade .NET before retrying
- If older version: Install .NET 8.0+ from https://dotnet.microsoft.com/download

---

## What Agent Does Next

✅ **After successful installation:**
- Agent automatically verifies packages in `YourProject.csproj`
- Agent confirms `dotnet list package` output shows Syncfusion packages
- Agent confirms no errors in installation log

**→ Auto-advance to Stage 7: Code Generation** (immediately after success)

---

## When Installation Fails

❌ **If installation fails after retries:**
- Agent reports specific error with context
- Agent provides user guidance for the error type
- Agent waits for user to resolve (e.g., upgrade .NET, check permissions)
- User confirms when ready to retry
- Agent retries installation automatically

