# Stage 7: Code Generation (Master Index)

**Purpose:** Generate clean, production-ready Razor Pages with Syncfusion components.

**Note:** This stage runs AFTER Stage 6 (packages installed).

---

## Quick Navigation

Before you start coding, follow this sequence in order:

### 1. **[Tag Helper Syntax Rules](tag-helper-syntax-rules.md)** (CRITICAL — 15 min read)
**Why first:** These 6 rules prevent 90% of build failures.

- Rule 1: Tag names — no hyphens except first
- Rule 2: Nested tags — parent-prefixed children
- Rule 3: Attributes — camelCase (no hyphens)
- Rule 4: Content — wrap in templates
- Rule 5: Data binding — use @Model, not ViewBag
- Rule 6: Unsupported tags — use attributes instead

**Read this BEFORE anything else.** Memorize the rules.

---

### 2. **[Component Skill Reference](component-skill-reference.md)** (CRITICAL — 20 min read)
**Why second:** Learn HOW to read component skill files (the authoritative source).

- Skill file locations and naming
- 4-step process: Extract → Read → Verify → Generate
- Common patterns (grids, forms, enums)
- What NOT to do (avoid guessing)

**Complete this step BEFORE reading any component skill file.**

---

### 3. **[Pre-Generation Checklist](pre-generation-checklist.md)** (10 sections)
**Why third:** Verify you're ready before writing a single line of code.

- Section 1: Skill reading verification
- Section 2: Tag syntax from skill files
- Section 3: Data binding (@Model patterns)
- Section 4: Namespaces and @using statements
- Section 5: Layout and HTML structure
- Section 6: Syncfusion component rules
- Section 7: CSS standards
- Section 8: File organization
- Section 9: Common build errors
- Section 10: Final readiness check

**All 10 sections MUST be complete before code generation.**

---

### 4. **[Code Generation Workflow](code-generation-workflow.md)** (30 min read)
**Why fourth:** Detailed process for generating all 3 files.

- Phase 1: Generate Razor Page (.cshtml)
  - Enum resolution in tag helpers
  - @using statements
  - Tag helper syntax
  
- Phase 2: Generate PageModel (.cs)
  - Properties and data binding
  - OnGet() and OnPost() handlers
  - Data models
  
- Phase 3: Generate Professional CSS
  - CSS variables
  - Mobile-first responsive design
  - Component styling
  - Accessibility standards
  
- Phase 4: Verification
  - Build and run checks

---

### 5. **[UI/CSS Design Standards](ui-css-design-standards.md)** (Reference)
**Why for reference:** Professional design standards that apply to ALL pages.

- Layout structure
- Form styling (login, registration, etc.)
- Color scheme (primary, neutral, semantic)
- Spacing & 8px grid system
- Typography hierarchy
- Syncfusion component styling
- Complete login page example

**Use this to ensure professional UI quality.**

---

### 6. **[Layout Standards](layout-standards.md)** (Reference)
**Why for reference:** Reusable layout patterns for all page types.

- 4 layout types (full-width, sidebar+content, header+content, three-column)
- Responsive design patterns
- Header component standard
- Sidebar navigation pattern
- Content grids
- Card component standard
- Syncfusion integration

**Use this for layout structure when creating pages.**

---

## Workflow (In Order)

```
START HERE
    ↓
Read: Tag Helper Syntax Rules
    ↓
Read: Component Skill Reference (HOW to read skills)
    ↓
Extract Components from component-mapping.json
    ↓
Read: EVERY component skill file
    ↓
Complete: Pre-Generation Checklist (all 10 sections)
    ↓
READY TO CODE
    ↓
Follow: Code Generation Workflow
    ↓
Generate: Razor Page (.cshtml)
    ↓
Generate: PageModel (.cs)
    ↓
Generate: Professional CSS
    ↓
Run: Verification (build, run, test)
    ↓
DONE ✅
```

---

## Critical Rules Summary

### The 6 Tag Helper Rules (from tag-helper-syntax-rules.md)

1. **Tag Names** → `<e-[component]-[no-hyphens-here]>`
2. **Child Tags** → `<e-[parent]-[child]>` (must include parent prefix)
3. **Attributes** → `attributeName="value"` (camelCase, no hyphens)
4. **Content** → Wrap HTML in `<e-*-template>` before adding markup
5. **Data Binding** → Use `@Model.Property` (Razor Pages), NOT ViewBag
6. **Configuration** → Use attributes, NOT unsupported nested tags

**Violating ANY rule causes RZ2010 or CS0117 build errors.**

---

## Common Mistakes (Do NOT do these)

❌ Invent tag names from memory (use skill files)  
❌ Guess attribute names (use skill file examples)  
❌ Use hyphenated attribute names (convert to camelCase)  
❌ Use ViewBag in Razor Pages (use @Model instead)  
❌ Put HTML directly in components (wrap in `<e-*-template>`)  
❌ Skip reading any component skill file  
❌ Assume syntax exists without verification  
❌ Generate code without completing pre-generation checklist  

**One mistake = build failure = time wasted. Be thorough.**

---

## File Structure

After code generation, your page will have 3 files:

```
Pages/
  [PageName]/
    Index.cshtml              ← Razor page with UI
    Index.cshtml.cs           ← PageModel with logic

wwwroot/css/
  [page-name].css             ← Professional styling
```

All 3 files MUST be present and correct for the page to function.

---

## Next Steps(VERY CRUSIAL - DON'T IGNORE)

1. **Start with:** [tag-helper-syntax-rules.md](tag-helper-syntax-rules.md)
2. **Then read:** [component-skill-reference.md](component-skill-reference.md)
3. **Then verify:** [pre-generation-checklist.md](pre-generation-checklist.md) (all sections)
4. **Then generate:** [code-generation-workflow.md](code-generation-workflow.md)
5. **Reference for UI:** [ui-css-design-standards.md](ui-css-design-standards.md)
6. **Reference for layout:** [layout-standards.md](layout-standards.md)

---

## Reference Files Index

| File | Purpose | Read Time |
|------|---------|-----------|
| [tag-helper-syntax-rules.md](tag-helper-syntax-rules.md) | 6 critical rules that prevent build failures | 15 min |
| [component-skill-reference.md](component-skill-reference.md) | How to read and extract from component skill files | 20 min |
| [pre-generation-checklist.md](pre-generation-checklist.md) | 10-section verification before code generation | 10 min |
| [code-generation-workflow.md](code-generation-workflow.md) | Detailed process for all 3 generated files | 30 min |
| [ui-css-design-standards.md](ui-css-design-standards.md) | Professional UI/CSS standards for all pages | Reference |
| [layout-standards.md](layout-standards.md) | Reusable layout patterns for different page types | Reference |

---

## Time Commitment

**First time through:**
- Read tag helper rules: 15 min
- Read skill reference guide: 20 min
- Read component skill files: 20-30 min
- Complete pre-generation checklist: 10 min
- Generate code with workflow: 30-45 min
- **Total: 95-120 minutes for first page**

**Subsequent pages:**
- Complete checklist: 5 min
- Generate code: 15-20 min
- **Total: 20-25 minutes per additional page**

---

## Success Criteria

✅ Code compiles without errors (`dotnet build`)  
✅ Application runs without errors (`dotnet run`)  
✅ Page displays correctly in browser  
✅ Forms work (inputs, buttons, validation)  
✅ Responsive design works on mobile/tablet/desktop  
✅ Accessibility verified (keyboard navigation, screen readers)  
✅ Color contrast ≥ 4.5:1 (WCAG AA)  
✅ Syncfusion components display correctly  
✅ CSS styling professional and consistent  

---

## Getting Help

If you encounter:

- **Build errors** → Check [tag-helper-syntax-rules.md](tag-helper-syntax-rules.md) for RZ2010/CS0117 errors
- **Component questions** → Read that component's skill file in `<skill-name>/SKILL.md`
- **Design questions** → Reference [ui-css-design-standards.md](ui-css-design-standards.md)
- **Layout questions** → Reference [layout-standards.md](layout-standards.md)
- **Attribute names** → Check the component's SKILL.md file (not assumptions)
- **Form patterns** → See [code-generation-workflow.md](code-generation-workflow.md) Phase 2 & 3

**When in doubt, read the skill file. It's the source of truth.**
