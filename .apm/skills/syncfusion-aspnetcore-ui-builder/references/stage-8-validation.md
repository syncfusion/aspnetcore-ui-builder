# Stage 8: Validation

**Purpose:** Validate generated code against web standards. Binary pass/fail result.

**AI Should:**

1. **Validate WCAG 2.1 AA Compliance:**
   - Semantic HTML structure used? (`<form>`, `<label>`, `<input>`, `<button>` tags)
   - ARIA labels on form fields?
   - Keyboard navigation supported? (tab order, focus management)
   - Color contrast ≥ 4.5:1 for text?
   - Focus indicator visible on interactive elements?

2. **Check Security:**
   - No XSS vulnerabilities (Razor auto-escapes by default)
   - No hardcoded secrets/API keys
   - Input validation on server-side
   - Antiforgery token present on forms

3. **Verify Performance:**
   - No unnecessary large script imports
   - CSS loaded in proper order
   - Minimal inline styles

4. **Check Responsive Design:**
   - Mobile-first approach (320px+)
   - Flexbox/Grid used for layouts?
   - Media queries for breakpoints?
   - Touch targets ≥ 44x44px?

5. **Verify Syncfusion Integration:**
   - Tag helpers properly registered in _ViewImports.cshtml
   - Theme CSS and Syncfusion JS loaded in _Layout.cshtml `<head>`
   - `<ejs-scripts></ejs-scripts>` present before `</body>` tag in _Layout.cshtml
   - NuGet package installed (Syncfusion.EJ2.AspNet.Core)
   - CSS/JS CDN version matches NuGet version

**Validation Result:**

Binary: **PASS ✓** or **FAIL ✗**

**If PASS:**
```
✓ Validation Result: PASS

All standards met:
  ✓ WCAG 2.1 AA accessibility
  ✓ Security checks (Razor auto-escape, antiforgery)
  ✓ Performance standards
  ✓ Responsive design
  ✓ Syncfusion integration
  ✓ Code quality

Ready to proceed to dependencies...
```

**If FAIL:**
```
✗ Validation Result: FAIL

Issues found:
  ✗ Color contrast on label text (3.2:1, need 4.5:1)
  ✗ Form inputs missing aria-describedby attributes

Auto-fixes applied:
  ✓ Increased font size for contrast
  ✓ Added aria-describedby to inputs

Remaining issues: 0
Result: PASS (after fixes)
```

**User Interaction:**

If result is PASS: Proceed to next stage - NO Confirmation needed.

If result is FAIL (after fixing):
```
Validation failed with 2 issues (not auto-fixable):
  - Form requires aria-live region for errors
  - Need custom input styling

Override and proceed anyway?
[Override & Proceed] [Request Manual Fixes] [Stop]
```

**Status:** User confirms validation result or overrides upon failures.

**Reference:** See web-standards.md for complete validation rules and correction methods.

---

## Build Failure Diagnostics (CRITICAL)

**When `dotnet build` fails, ALWAYS follow this protocol. Do NOT skip skill file verification.**

### Build Failure Response Protocol (Mandatory Steps)

**IF build fails with error → IMMEDIATELY:**

1. **Identify the error type** (RZ2010, CS0117, CS1061, etc.)
2. **Extract the component name** from the error
3. **Find component in components.csv** (`.apm/skills/syncfusion-aspnetcore-ui-builder/scripts/components.csv`)
4. **Read that component's SKILL.md file** from the skill path listed in components.csv
5. **Compare generated code** against skill file examples
6. **Fix mismatched syntax** based on skill file (not guesses)
7. **Rebuild and verify**

### Common Build Errors & Diagnostics

#### Error: RZ2010 (Unexpected tag)
**Cause:** Incorrect tag name format or unsupported nested element

**Diagnostic Steps:**
1. Extract component name from error (e.g., "TextBox")
2. Search `components.csv` for exact name match
3. **Read skill file** for that component
4. Compare generated tag against skill examples
5. Check Rule 1 from tag-helper-syntax-rules.md (tag naming)

**Common Fixes:**
- ❌ `<ejs-textinput>` → ✅ Read skill to find correct: `<ejs-textbox>`
- ❌ `<e-columns>` → ✅ Should be: `<e-grid-columns>`
- ❌ Custom nested tags → ✅ Use attributes instead per skill examples

#### Error: CS0117 (Does Not Contain)
**Cause:** Attribute name mismatch or unsupported enum

**Diagnostic Steps:**
1. Extract attribute/enum name from error
2. Find component in `components.csv`
3. **Read skill file** for that component
4. Search skill examples for that attribute
5. Copy exact attribute name (camelCase) from skill

**Common Fixes:**
- ❌ `allowsort="true"` → ✅ Check skill: `allowSorting="true"`
- ❌ `DataSource` attribute → ✅ Use `dataSource` (camelCase)
- ❌ Enum without namespace → ✅ Add namespace prefix: `Syncfusion.EJ2.Grids.GridTextAlign.Right`

#### Error: CS1061 (Model Does Not Contain)
**Cause:** PageModel property mismatch or undefined

**Diagnostic Steps:**
1. Extract property name from error
2. Verify property defined in PageModel
3. Check spelling and casing (C# is case-sensitive)
4. Ensure property is marked with `[BindProperty]` for forms
5. Verify property type matches usage

**Common Fixes:**
- ❌ `@Model.Items` (property doesn't exist) → ✅ Define in PageModel: `public List<Item> Items { get; set; }`
- ❌ `@Model.item` → ✅ Should be: `@Model.Item` (capitalization)
- ❌ Form input not bound → ✅ Add `[BindProperty]` to PageModel property

### Build Failure Decision Tree

```
Build fails
    ↓
Error type = ?
    ├─ RZ2010 → Tag/element error
    │   ├─ Find component in components.csv
    │   ├─ Read SKILL.md for that component
    │   └─ Compare tag names against skill examples
    │
    ├─ CS0117 → Attribute/enum error
    │   ├─ Find component in components.csv
    │   ├─ Read SKILL.md for that component
    │   └─ Find exact attribute name in skill examples
    │
    ├─ CS1061 → Model property error
    │   ├─ Check PageModel for property definition
    │   ├─ Verify spelling and casing
    │   └─ Add property if missing with correct type
    │
    └─ Other → Check Razor syntax, namespaces, etc.

After fix:
    ↓
Re-check component skill?
    ├─ YES → Read skill again, verify syntax
    └─ NO → Rebuild

Rebuild succeeds?
    ├─ YES → Proceed to next page
    └─ NO → Repeat diagnostic process
```

### What NOT To Do During Build Failure ⭐ IMPORTANT

❌ **DO NOT:**
- Guess tag or attribute names
- Modify syntax without checking skill file
- Skip reading component skill files
- Assume a component doesn't support something
- Continue without fixing the error
- Use default HTML controls instead of checking for Syncfusion equivalent
- Ignore error messages

✅ **DO:**
- Read the error message carefully
- Find component in `components.csv`
- Read that component's SKILL.md file
- Compare generated code against skill examples
- Fix syntax based on skill file evidence
- Test rebuild after each fix
- Ask user for confirmation before using non-Syncfusion controls

### Skill File Reference is MANDATORY

**Every build error requires consulting the relevant component skill file.**

The skill file is the **source of truth** for:
- Correct tag names and format
- Supported attributes and values
- Enum names and namespaces
- Data binding patterns
- Server-side setup requirements
- Nested element structures

**Never modify Syncfusion component syntax without skill file confirmation.**

---

## Validation Proof Across All Page Types

**This design system works universally across different web page types.**

The following test cases demonstrate that UI/CSS standards validate successfully for:
- Login/Authentication pages
- Dashboards/Analytics pages  
- Product listing pages
- Data table/CRUD pages
- Form/Survey pages
- Report/Summary pages
- Admin/Settings pages

### Coverage Matrix

| Page Type | Colors | Typography | Spacing | Forms | Buttons | Tables | Responsive | Accessibility | Status |
|-----------|--------|-----------|---------|-------|---------|--------|-----------|----------------|--------|
| Auth/Login | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ | PASS |
| Dashboard | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | PASS |
| Product List | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ | PASS |
| CRUD/Table | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | PASS |
| Form/Survey | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ | PASS |
| Report | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | PASS |
| Settings | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ | PASS |

### Verified Universal Standards

✅ **Color System** — Works with all page types (primary, secondary, semantic colors)  
✅ **Typography** — Proper hierarchy (h1-h4) fits all layouts  
✅ **Spacing** — 8px grid system scales to any layout  
✅ **Forms** — Input/label/help patterns work universally  
✅ **Buttons** — Primary/secondary/danger variants useful everywhere  
✅ **Responsive** — Mobile-first breakpoints (320px, 640px, 1024px, 1280px)  
✅ **Accessibility** — Focus states, contrast, ARIA support across all types  
✅ **Syncfusion Integration** — Grid, Charts, Dropdowns, TextBox all styled  

### Page Type Examples

For detailed examples showing how validation works across all page types, see the attachments or refer to the complete validation reference document. Each page type includes:
- HTML structure demonstrating universal standards application
- CSS patterns that apply across page types
- Verification checklist showing which standards are active

**All page types pass validation when using the UI/CSS Design Standards defined in [stage-5-code-generation.md](stage-5-code-generation.md).**
