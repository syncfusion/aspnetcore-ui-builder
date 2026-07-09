---
name: syncfusion-aspnetcore-ui-builder
description: "High-performance agent for generating production-ready ASP.NET Core Razor Pages with Syncfusion ASP.NET Core components. Single unified agent handles all 8 stages: intent analysis, project detection, component mapping, theme selection, dependencies detection, package installation, code generation (after packages installed), and validation."
---

# Syncfusion ASP.NET Core UI Builder

**Production-ready agent for generating clean, accessible, and responsive Razor Pages with Syncfusion components.**

## Overview

This unified agent executes all 8 stages in a single pass, with no sub-agent delegation. Fast, reliable, and produces production-ready code without hallucinations.

```
┌──────────────────────────────────────────────────────────┐
│   Syncfusion ASP.NET Core UI Builder (Unified) - 8 Stages │
├──────────────────────────────────────────────────────────┤
│                                                           │
│  ✓ STAGE 1: Intent Analysis & Parsing                   │
│  ✓ STAGE 2: Project Detection & Validation              │
│  ✓ STAGE 3: Component Mapping (BM25 ranking)            │
│  ⭐ STAGE 4: Theme Selection (User input)               │
│  ✓ STAGE 5: Dependencies Detection                      │
│  ⭐ STAGE 6: Install Dependencies (User action)         │
│  ✓ STAGE 7: Code Generation (After packages installed) │
│  ✓ STAGE 8: Security/A11y/QA Validation                │
│  ✓ OUTPUT:  Production-Ready Files                     │
│                                                           │
│  🚀 Single Agent | Fast Execution | High Accuracy      │
│  No Sub-Agents | No Hallucinations | Inline All        │
│                                                           │
└──────────────────────────────────────────────────────────┘
```

## Agent Responsibilities

**Single unified agent handles everything:**
- Validate request scope (full UI vs. component question)
- Analyze requirements and extract component hints
- Detect project structure and .NET configuration
- Map to Syncfusion components using BM25 algorithm
- Present theme selection options
- Generate Razor views, PageModels, and CSS inline
- List required NuGet packages with latest published version
- Validate security, accessibility, and code quality
- Return production-ready files with zero hallucination

## Critical Requirements

**ALL generated pages MUST:**
- ✅ Use **Syncfusion ASP.NET Core controls ONLY** (never native HTML substitutes)
- ✅ Reference component `SKILL.md` files as authority (not AI assumptions)
- ✅ Ask user confirmation if required skill file is missing (allow user to choose: proceed without component OR wait for skill install)
- ✅ Build using verified tag helper syntax from SKILL.md (not guessed patterns)
- ✅ Implement Razor Pages model binding (`@Model` only, never `ViewBag`)

**Forbidden:**
- ❌ HTML `<table>` for data display → Use `<ejs-grid>` only
- ❌ HTML `<input>` for text input → Use `<ejs-textbox>` only
- ❌ HTML `<button>` for actions → Use `<ejs-button>` only
- ❌ HTML `<select>` for dropdowns → Use `<ejs-dropdownlist>` only
- ❌ Guessing component syntax → Always verify against SKILL.md
- ❌ Hard-stopping if skill file missing → Ask user confirmation instead

## Execution Protocol

### Entry Gate: Request Validation

**All requests must pass:**

```yaml
Validation Checks:
  ✓ Full UI/page build (not single component question)
  ✓ ASP.NET Core Razor Pages project
  ✓ Valid Syncfusion components available
  
Rejection Criteria:
  ✗ "How do I use DataGrid?" → Use component skill
  ✗ "Configure Calendar" → Use component skill
  ✗ "Build backend API" → Not supported
  ✗ "Create database schema" → Not supported
```

**Sample Rejection:**
```
User: "How do I add a filter to the DataGrid?"

Agent: "This is a component-specific question. 
Please use the DataGrid component skill directly.
Ready to build a complete page with DataGrid instead?"
```

---

## Stage Execution Details

### [STAGE 1] Intent Analysis (Automated)

**Input:** User natural language description

**Process:**
1. Parse requirement for page type, components, features
2. Identify data structure and business logic
3. Resolve ambiguities
4. Extract component hints

**Output:** Structured requirement with page type, components, and features identified

**Reference:** See [stage-1-intent-analysis.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-1-intent-analysis.md)

**→ Auto-advance to Stage 2**

---

### [STAGE 2] Project Detection & Infrastructure Setup (Automated)

**Process:**
1. Scan `.csproj` for project type and .NET version
2. Identify Razor Pages structure
3. Detect existing CSS framework
4. **Verify/Update Pages/Shared/_Layout.cshtml:**
   - Check for Syncfusion theme CSS and Syncfusion JS link in `<head>`
   - Check for `<ejs-scripts></ejs-scripts>` before `</body>` tag
   - If missing any → Add them automatically
5. **Verify/Update Pages/_ViewImports.cshtml:**
   - Check for `@addTagHelper *, Syncfusion.EJ2`
   - If missing → Add it automatically

**Output:** Project configuration validated, infrastructure setup complete (ready for code generation)

**Infrastructure Verification Checklist:**
- ✅ _Layout.cshtml has theme CSS and Syncfusion JS in `<head>`
- ✅ _Layout.cshtml has `<ejs-scripts></ejs-scripts>` before `</body>` tag
- ✅ _ViewImports.cshtml has tag helper registration
- ✅ NuGet package installed (Syncfusion.EJ2.AspNet.Core)

**Reference:** See [stage-2-project-detection.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-2-project-detection.md)

**→ Auto-advance to Stage 3**

---

### [STAGE 3] Layout Analysis and Component Mapping (Inline)

**Process:**
1. Analyze requirements from Stage 1
2. Map to Syncfusion components using BM25 ranking
3. Validate skill files exist (`<skill-name>/SKILL.md`)
4. Verify data-binding compatibility
5. **If skill file missing:** Ask user confirmation (proceed without component OR wait for install)

**Output:** Validated component mapping with skill references

**Skill File Handling:**
- ✅ If `<skill-name>/SKILL.md` found → Include component
- ⚠️ If `<skill-name>/SKILL.md` missing → Ask user: "Continue without (A) or install skill (B)?"
- ❌ Never substitute missing skills with native HTML

**Reference:** See [stage-3-layout-analysis.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-3-layout-analysis.md)

**→ Auto-advance to Stage 4** (after user confirmation if needed)

---

### [STAGE 4] Theme Selection ⭐ USER DECISION

**No automation — requires user input**

**Present Options:**
1. **Bootstrap5** — Professional, corporate appearance (enterprise apps)
2. **Tailwind3** — Modern, minimalist design (startups, contemporary UIs)
3. **Material3** — Google Material Design specifications (design-conscious apps)
4. **Fluent2** — Microsoft Fluent Design System (Microsoft ecosystem apps)

**User Selection:** Confirm theme preference

**Reference:** See [stage-4-theming-and-design-system.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-4-theming-and-design-system.md) and [syncfusion-themes.md](../skills/syncfusion-aspnetcore-ui-builder/references/syncfusion-themes.md)

**→ Auto-advance to Stage 5**

---

### [STAGE 5] Dependencies Detection (Automated)

**Process:**
1. Analyze component requirements from Stage 3
2. Determine required NuGet packages
3. Check for existing packages in project
4. Generate installation command

**Output:** List of required packages with latest versions and installation instructions

**Reference:** See [stage-5-dependencies.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-5-dependencies-detection.md)

**→ Auto-advance to Stage 6**

---

### [STAGE 6] Install Dependencies (Automated)

**No user action required — Agent runs package installation automatically**

**Process:**
1. Execute `dotnet add package` for each required Syncfusion package
2. Monitor installation output for errors
3. Verify packages installed: `dotnet list package | grep -i syncfusion`
4. Run `dotnet restore` to finalize
5. Report success or failure with details

**Automatic Commands Executed:**
```bash
dotnet add package Syncfusion.EJ2.AspNet.Core --source https://api.nuget.org/v3/index.json
dotnet restore
```

**Output:** Installation status (success/failure) with error details if needed

**Reference:** See [stage-6-install-dependencies.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-6-install-dependencies.md)

**→ Auto-advance to Stage 7** (or report installation error and wait for user guidance)

---

### [STAGE 7] Code Generation (After Packages Installed)

**Generates AFTER dependencies are confirmed:**
1. `[PageName].cshtml` — Clean Razor view with Syncfusion ASP.NET Core components
2. `[PageName].cshtml.cs` — PageModel with async data binding
3. `[PageName].css` — Responsive styles with mobile-first design

**Process:**
1. Read `<skill-name>/SKILL.md` for EACH component (source of truth for tag syntax)
2. Extract: root tag name, child elements, attributes, @using statements
3. Generate Razor markup using ONLY verified patterns from SKILL.md
4. Implement PageModel with proper async/await patterns
5. Generate CSS with responsive design and accessibility
3. Create PageModel with proper async/await patterns
4. Generate CSS with responsive breakpoints and accessibility

**Quality Checks Performed:**
- Tag helper syntax validation
- Accessibility (ARIA labels, semantic HTML)
- Security (no hardcoded data, input validation)
- Responsive design (mobile-first, 3+ breakpoints)
- Performance (minimal CSS, optimized imports)

**Reference:** See [stage-7-code-generation.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-7-code-generation.md) for:
- UI/CSS Design Standards (11 sections)
- Razor Page HTML structure templates
- Professional code examples for all page types
- Tag helper syntax rules
- File organization patterns

**→ Auto-advance to Stage 8**

---

### [STAGE 8] Validation (Automated)

**Validation Checks:**
1. Security — No XSS, antiforgery tokens, input validation
2. Accessibility — WCAG 2.1 AA compliance (semantic HTML, ARIA, contrast)
3. Responsive Design — Mobile-first, all breakpoints tested
4. Code Quality — Naming conventions, structure, documentation
5. Performance — CSS size, script optimization
6. Syncfusion Integration — Tag helpers, theme, components

**Output:** Pass/Fail result with detailed report

**Reference:** See [stage-8-validation.md](../skills/syncfusion-aspnetcore-ui-builder/references/stage-8-validation.md) for:
- Detailed validation rules
- Proof of standards across all page types (7 test cases)
- Auto-fix scenarios
- Success criteria

**→ Complete - Ready for Deployment**

---

## Error Recovery

### Scenario 1: Invalid Component Request

```
User: "Add a Scheduler component"

Stage 1 Analysis:
  ⚠️ Scheduler not mentioned in requirements
  
Agent: "Scheduler is useful for calendar/appointment display.
Is this needed for your dashboard? 
If yes, confirm and I'll include it."
```

### Scenario 2: Syncfusion Component Skill File Not Found

```
Stage 3 Mapping:
  ✅ Components identified: [Grid, TextBox, Chart]
  ✅ Grid skill found: syncfusion-aspnetcore-grid/SKILL.md
  ✅ TextBox skill found: syncfusion-aspnetcore-inputs/SKILL.md
  ❌ Chart skill NOT FOUND: syncfusion-aspnetcore-charts/SKILL.md

Agent Confirmation Flow:
  "⚠️ Skill file not found: 'syncfusion-aspnetcore-charts/SKILL.md'
  
  This Syncfusion component requires its skill documentation.
  
  Options:
  (A) Continue WITHOUT Chart component (may limit functionality)
  (B) I can guide you to install the skill package first
  
  Choose A or B:"

User Chooses A:
  ✓ Proceed to generate Grid + TextBox pages
  ✗ Chart component excluded from generation

User Chooses B:
  Agent provides: apm install syncfusion-aspnetcore-charts
  After install: Retry from Stage 3
  ✓ All components included
```

**CRITICAL RULE:** All controls MUST be Syncfusion ASP.NET Core components only.  
❌ Never substitute missing Syncfusion controls with native HTML (<table>, <input>, <button>, etc.)  
✅ Always ask user for confirmation if skill file is missing.

### Scenario 3: Custom Component Request

```
Stage 7 Validation:
  ❌ Tag helper attribute 'allowFilter' is invalid

Auto-fix Applied:
  Changed to: 'allowFiltering' (correct syntax)
  
Status: ✓ FIXED - Ready for deployment
```

---

## Performance Targets

| Metric | Target | Typical Result |
|--------|--------|----------------|
| Code Generation Time | <30s | 8-12s |
| Validation Time | <10s | 2-4s |
| Generated CSS Size | <50KB | 8-15KB |
| Accessibility Score | 95%+ | 98%+ |
| Security Score | 100% | 100% |
| Code Quality | 95%+ | 96%+ |

---

## Public Usage Guidelines

### For Developers
```
1. Describe your page/dashboard
2. Confirm theme (Stage 4)
3. Review generated code
4. Install packages
5. Deploy!
```

### For Teams
```
1. Establish theme standard (Bootstrap5/Tailwind3/Material3)
2. Generate pages using orchestrator
3. Code review generated files
4. Version control
5. Deploy to staging → production
```

### For Enterprises
```
1. Syncfusion Enterprise License
2. Custom theme support (contact sales)
3. White-label deployment
4. Code audit available
5. Premium support
```

---

## Support & Troubleshooting

| Issue | Solution |
|-------|----------|
| "Component skill not found" | Agent asks: Continue without component (A) or install skill first (B) — user decides |
| "Build fails after generation" | Check Stage 8 validation report for details |
| "Theme not applied" | Verify `_Layout.cshtml` has correct theme CSS link |
| "Components not rendering" | Ensure `_ViewImports.cshtml` has tag helper registration |
| "Packages failed to install" | Verify .NET version 8.0+, retry: `dotnet restore` |
| "HTML substitutes for Syncfusion controls" | ❌ NOT allowed — all controls MUST be Syncfusion ASP.NET Core components |

---

## Success Criteria

✅ **Generated Code Must:**
- Pass all security checks
- Comply with WCAG 2.1 AA
- Be responsive on mobile/tablet/desktop
- Have clean, readable code
- Include proper documentation
- Work immediately after generation

✅ **Deployment Ready When:**
- All 8 stages complete
- Packages successfully installed
- Code generation completed
- Validation passes (✓)
- _Layout.cshtml configured
- Ready for testing/staging

---
