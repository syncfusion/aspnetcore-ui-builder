# Pre-Generation Checklist

**Complete verification before writing ANY Razor code. MUST pass all items.**

---

## Section 1: Skill Reading (BLOCKED until complete)

Before proceeding to code generation, verify all component skills have been read:

### Components Identified
- [ ] Listed all unique skills from `component-mapping.json`
- [ ] Counted total unique skills required
- [ ] Documented each skill name and file path

### Skills Read
- [ ] Read `<skill-name>/SKILL.md` for EVERY skill
- [ ] Confirmed each file existed (OR asked user for confirmation if missing)
- [ ] **If any skill file missing:** Asked user (A: Continue without component OR B: Install skill first)
- [ ] Built skill reference table (root tag, children, attributes) from what was read
- [ ] No skill was skimmed — fully read each file

### Skill Reference Table Built
For each component, verified and documented:
- [ ] Root tag helper name (e.g., `<ejs-grid>`)
- [ ] All child element names used in examples
- [ ] All attribute names used in examples (camelCase, exact spelling)
- [ ] Required `@using` statements
- [ ] Required NuGet package
- [ ] Server-side setup patterns (PageModel properties, initialization)

---

## Section 1.5: Component Validation Against components.csv (MANDATORY)

**ALL controls must be Syncfusion ASP.NET Core components. DO NOT use HTML controls without explicit user confirmation.**

### Component Library Reference
- [ ] Opened: `.apm/skills/syncfusion-aspnetcore-ui-builder/scripts/components.csv`
- [ ] Verified: EVERY component from `component-mapping.json` exists in `components.csv`
- [ ] Documented: Skill name for each component (from `components.csv` column 3)
- [ ] NO component is missing or undefined

### Syncfusion Control Verification
For each identified component:
- [ ] ✅ Listed in `components.csv` as Syncfusion component
- [ ] ✅ Skill name and path documented
- [ ] ✅ Tag helper name format confirmed (`ejs-*`)
- [ ] ✅ NOT a default HTML control (input, button, div, etc.)

### HTML Control Rule ⭐ MANDATORY
- [ ] **Default HTML controls are NOT allowed without user confirmation**
- [ ] Examples of disallowed controls WITHOUT confirmation:
  - ❌ `<input type="text">` (use `<ejs-textbox>` instead)
  - ❌ `<button>` (use `<ejs-button>` instead)
  - ❌ `<select>` (use `<ejs-dropdown-list>` instead)
  - ❌ `<textarea>` (use `<ejs-richtexteditor>` instead)
  - ❌ `<table>` (use `<ejs-grid>` instead)

### If HTML Control Needed
1. **STOP code generation immediately**
2. **Ask user:** "Component X is not available as Syncfusion control. Should I:"
   - A) Use Syncfusion alternative [name] instead?
   - B) Use HTML [tag] with your explicit confirmation?
   - C) Skip this component and re-check skills?
3. **Document user's choice** in conversation
4. **Re-verify skills** if user chose (C)
5. **Proceed with caution** if user chose (B) — mark as exception

### When to Re-Check Skills
If a component seems unavailable:
1. **Search components.csv** for alternative names
2. **Read the component skill file** for exact usage
3. **Ask user:** "Should we use [alternative] instead?" BEFORE generating
4. **Never assume** a component doesn't exist — check the skill first

### Build Failure Response Protocol
**If build fails, ALWAYS check relevant component skill files FIRST:**
1. Note the error component name
2. Find that component in `components.csv`
3. Read its SKILL.md file carefully
4. Compare generated code against skill examples
5. Fix mismatched tag/attribute names
6. **Do NOT guess or modify syntax without skill file reference**

---

## Section 2: Tag Syntax Verification

**Verify ALL tag syntax will be taken from skill files, NOT from memory.**

### Root Tags (from skill files ONLY)
- [ ] Root tag names extracted from skill file examples
- [ ] No tag names invented from AI training knowledge
- [ ] Exact tag names ready for copy-paste from skills
- [ ] No component will use incorrect tag syntax

### Child Elements (from skill files ONLY)
- [ ] Child tag names extracted from skill file examples
- [ ] Every child confirmed to start with `<e-[parent]-...>` pattern
- [ ] Parent names verified against root tag names
- [ ] No child elements invented or assumed

### Attributes (from skill files ONLY)
- [ ] All attribute names in camelCase (not hyphenated)
- [ ] Attribute names verified from skill file examples
- [ ] No attributes invented that weren't in examples
- [ ] Required attributes identified
- [ ] Optional attributes identified
- [ ] Attribute values and types confirmed

### Nested Tags
- [ ] Confirmed which child elements are supported
- [ ] Identified unsupported nested configuration tags (e.g., `<e-*-events>`)
- [ ] No unsupported tags will be used
- [ ] Template wrappers (`<e-content-template>`) identified for HTML content

---

## Section 3: Data Binding Verification

**Ensure @Model is used correctly for Razor Pages (NOT ViewBag).**

### Model Properties
- [ ] All PageModel properties identified
- [ ] Properties marked with `[BindProperty]` for form inputs
- [ ] Collections initialized (e.g., `= new()`)
- [ ] Public property names match `@Model` bindings

### Razor Page Bindings
- [ ] All data binding uses `@Model.PropertyName`
- [ ] NO `ViewBag` usage anywhere in Razor page
- [ ] NO bare property names without `@Model`
- [ ] Enum references use correct namespace prefix (e.g., `Dropdowns.FilterType`)

### PageModel Setup
- [ ] OnGet() handler initializes all data
- [ ] OnPost() handler defined for form submissions
- [ ] ModelState validation included
- [ ] Data model classes ready

---

## Section 4: Namespace & Using Statements

**Verify all required namespaces before code generation.**

### @using Statements Identified
- [ ] Base namespace: `@using Syncfusion.EJ2`
- [ ] Component-specific namespaces identified from skills
- [ ] Examples: `@using Syncfusion.EJ2.Grids`, `@using Syncfusion.EJ2.Inputs`
- [ ] Custom namespace for PageModel identified

### @using Placement
- [ ] All `@using` statements at top of Razor page (after `@page`)
- [ ] No duplicate namespaces
- [ ] Base `@using Syncfusion.EJ2` included for enum resolution

### PageModel Namespaces
- [ ] `using Microsoft.AspNetCore.Mvc`
- [ ] `using Microsoft.AspNetCore.Mvc.RazorPages`
- [ ] `using System.Collections.Generic`
- [ ] Custom namespace ready

---

## Section 5: Layout & HTML Structure

**Verify HTML structure and accessibility.**

### Semantic HTML
- [ ] `<main>` for main content with `role="main"`
- [ ] `<header>` for page header
- [ ] `<section>` for content sections
- [ ] `<footer>` for page footer
- [ ] Proper heading hierarchy (h1 → h2 → h3, etc.)

### Accessibility
- [ ] Form labels associated with inputs (`for` and `id` match)
- [ ] `aria-label` attributes for screen readers
- [ ] Focus indicators visible (CSS focus states)
- [ ] Color contrast ≥ 4.5:1 for text (WCAG AA)
- [ ] Interactive elements ≥ 44x44px (touch friendly)
- [ ] Keyboard navigation supported

### CSS Classes
- [ ] Container classes: `page-container`, `page-header`, `page-content`, `page-footer`
- [ ] Form classes: `form-container`, `form-group`, `form-label`, `form-input`
- [ ] Button classes: `btn`, `btn-primary`, `btn-block`
- [ ] No class names invented (consistent with design standards)

---

## Section 6: Syncfusion Components

**Verify all Syncfusion components follow syntax rules.**

### Tag Helper Names
- [ ] All root tags use `<ejs-[name]>` format
- [ ] All child tags use `<e-[parent]-[descriptor]>` format
- [ ] No hyphens in descriptors (except first hyphen)
- [ ] Verified against skill files (not assumed)

### Attributes
- [ ] All attributes in camelCase
- [ ] No hyphenated attribute names
- [ ] Data binding uses `@Model.PropertyName`
- [ ] Enum values use correct namespace (e.g., `Dropdowns.FilterType.Contains`)

### Content Wrapping
- [ ] HTML content wrapped in `<e-*-template>`
- [ ] No bare HTML inside component tags
- [ ] Template structure matches examples from skills

### Unsupported Tags
- [ ] No `<e-*-events>` configuration tags
- [ ] No unsupported nested configuration
- [ ] Using attributes for configuration (correct approach)

---

## Section 7: CSS Standards

**Verify professional CSS will be generated.**

### CSS Variables
- [ ] Color variables defined (primary, secondary, border, text)
- [ ] Spacing variables defined (8px grid system)
- [ ] Border radius variables defined
- [ ] All colors have CSS variable alternatives

### Responsive Design
- [ ] Mobile-first approach (base styles apply to all screens)
- [ ] Media queries at 640px, 1024px, 1280px
- [ ] Container padding adjusts for screen size
- [ ] Font sizes scale appropriately
- [ ] No fixed widths (use max-width instead)

### Component Styling
- [ ] Form inputs styled consistently
- [ ] Buttons have hover and active states
- [ ] Focus states visible (3px outline or equivalent)
- [ ] Syncfusion component overrides prepared
- [ ] Links underline on hover

### Color Contrast
- [ ] Primary text on background ≥ 4.5:1
- [ ] Secondary text on background ≥ 4.5:1
- [ ] Focus indicator ≥ 3:1 contrast
- [ ] Verified with color contrast tool

---

## Section 8A: Infrastructure Setup (CRITICAL)

**Verify Pages/Shared/_Layout.cshtml has ALL required Syncfusion elements.**

### _Layout.cshtml Head Section
- [ ] Theme CSS link present in `<head>`
  ```html
  <link rel="stylesheet" href="https://cdn.syncfusion.com/ej2/{version}/bootstrap5.css" />
  ```
- [ ] Syncfusion JS script present in `<head>` (after theme CSS)
  ```html
  <script src="https://cdn.syncfusion.com/ej2/{version}/dist/ej2.min.js"></script>
  ```
- [ ] Version matches installed NuGet package (e.g., 33.2.10)

### _Layout.cshtml Body Section (Before </body>)
- [ ] `<ejs-scripts></ejs-scripts>` tag present (CRITICAL)
  ```html
  <ejs-scripts></ejs-scripts>
  ```
- [ ] `<ejs-scripts>` is BEFORE `</body>` closing tag

### _ViewImports.cshtml
- [ ] Tag helper registration present: `@addTagHelper *, Syncfusion.EJ2`
- [ ] Located at: `Pages/_ViewImports.cshtml`

### NuGet Package
- [ ] Syncfusion.EJ2.AspNet.Core installed
- [ ] Version matches CDN URLs in _Layout.cshtml
- [ ] Run: `dotnet list package | grep -i syncfusion`

**⭐ If ANY of these are missing, pages will NOT render Syncfusion components!**

---

## Section 8: File Organization

**Verify proper file structure and naming.**

### File Names
- [ ] Razor page: `Pages/[ComponentName]/Index.cshtml`
- [ ] PageModel: `Pages/[ComponentName]/Index.cshtml.cs`
- [ ] CSS file: `wwwroot/css/[component-name].css`
- [ ] Naming follows ASP.NET Core conventions

### File Content
- [ ] Razor page contains `@page` directive
- [ ] Razor page has `@model` declaration
- [ ] PageModel file has `public class [Name]Model : PageModel`
- [ ] CSS file has proper header comments

### Directory Structure
- [ ] `Pages/` directory structure prepared
- [ ] `wwwroot/css/` directory ready for CSS
- [ ] No duplicate files
- [ ] Proper folder nesting if needed

---

## Section 8B: UI Glitch Prevention (IMPORTANT)

**Ensure CSS will prevent common UI display issues. Reference `ui-css-design-standards.md` sections 7-12.**

### Text Overflow & Truncation
- [ ] Page has elements with variable-length text (labels, titles, descriptions)
- [ ] Plan added: `.truncate-single` for single-line text with ellipsis
- [ ] Plan added: `.truncate-lines` for multi-line text (2-3 lines max)
- [ ] Plan added: `.text-wrap-safe` for safe word wrapping without overlap
- [ ] Log/code elements: `.log-text` with `white-space: pre-wrap` and `word-break`
- [ ] All table cells have `min-width: 0` for proper flex truncation

### Tree/List Components
- [ ] Tree/list component identified (from component mapping)
- [ ] Plan added: `.tree-item-text` with proper flex layout
- [ ] Plan added: Tree item labels will NOT be clipped (max-width constraints)
- [ ] Icons/expand buttons have fixed `min-width` (no flex-grow)
- [ ] Text overflow handled with `text-overflow: ellipsis`

### Image Sizing & Aspect Ratio
- [ ] Images identified: modal images, card images, thumbnails, product images
- [ ] Plan added: `.modal-image` with `object-fit: contain` (preserve aspect ratio)
- [ ] Plan added: `.card-image` with `object-fit: cover` (fill space properly)
- [ ] Plan added: `.product-image` with `aspect-ratio` property
- [ ] All images have `max-width: 100%` and `height: auto`
- [ ] Image containers prevent layout shift with padding-bottom technique

### Component Spacing & Alignment
- [ ] Appointment/schedule items identified
- [ ] Plan added: Flex layout with `gap` property (prevent time/status overlap)
- [ ] Appointment times: fixed `min-width`, right-aligned, `white-space: nowrap`
- [ ] Appointment status badges: `flex-shrink: 0`, no wrapping
- [ ] Grid rows: proper padding with `min-width: 0` on cells
- [ ] Card titles/descriptions: multi-line truncation with `-webkit-line-clamp`
- [ ] Modal content: `max-height: 90vh` with scrolling handled properly

### Border & Decoration Standards
- [ ] Card borders: 1px solid (no unwanted red/colored underlines)
- [ ] List item borders: bottom borders only (last item none)
- [ ] Links: controlled underlines (none by default, underline on hover)
- [ ] No text-decoration applied unintentionally to containers

### Responsive Overflow Handling
- [ ] Mobile breakpoint (max-width: 640px): text truncation adjusted
- [ ] Tablet breakpoint (640px-1024px): optimal spacing applied
- [ ] Desktop breakpoint (1024px+): full spacing with proper grid columns
- [ ] Font sizes adjusted per breakpoint
- [ ] Padding/gap adjusted for mobile vs desktop

---

## Section 9: Common Build Errors

**Identify potential errors BEFORE generation.**

### RZ2010 Errors (Tag Not Allowed)
- [ ] No invalid tag names (checked against skills)
- [ ] No hyphens in descriptors (except first)
- [ ] All child tags prefixed with parent name
- [ ] No invented tag structures

### CS0117 Errors (Does Not Exist)
- [ ] All enum references have correct namespace prefix
- [ ] All PageModel properties defined
- [ ] All `@using` statements present
- [ ] No typos in property names

### CS1061 Errors (Does Not Contain)
- [ ] All `@Model.Property` names match PageModel
- [ ] All properties are public
- [ ] No PropertyName typos
- [ ] Case-sensitive matching verified

---

## Section 10: Final Readiness Check

**Before clicking "generate," verify readiness:**

### Syncfusion Component Verification (MANDATORY) ⭐
- [ ] Opened `components.csv` and verified ALL components exist
- [ ] Each component from `component-mapping.json` is Syncfusion, not HTML default
- [ ] No HTML controls (input, button, select, textarea, table) without user confirmation
- [ ] If HTML control needed, user explicitly confirmed in conversation
- [ ] Documented: each component name → Syncfusion skill → correct tag format

### Knowledge Verified
- [ ] I have read ALL component skill files
- [ ] I understand the 6 tag helper syntax rules
- [ ] I know the exact tag names to use (from skills)
- [ ] I know the exact attribute names to use (from skills)
- [ ] I will NOT invent any syntax from memory
- [ ] **I will use ONLY Syncfusion controls (per components.csv)**
- [ ] **Build failure → I will consult skill files FIRST (mandatory protocol)**

### Preparation Complete
- [ ] Component mapping extracted
- [ ] Skill reference table built
- [ ] PageModel structure planned
- [ ] CSS design prepared
- [ ] File organization ready
- [ ] **Syncfusion components verified against components.csv**

### Ready to Generate
- [ ] All skill files read
- [ ] All checklist items complete (Sections 1-10)
- [ ] No components missing skill files
- [ ] _Layout.cshtml has theme CSS + scripts + `<ejs-scripts>`
- [ ] _ViewImports.cshtml has `@addTagHelper *, Syncfusion.EJ2`
- [ ] NuGet package installed and version verified
- [ ] No build errors anticipated
- [ ] **All controls are Syncfusion (verified in components.csv)**
- [ ] Ready to write production code

---

## Sign-Off (Mental Commitment)

Before code generation, confirm:

✅ **I have read ALL component skill files** (not skipped any)  
✅ **I understand tag helper syntax rules** (6 critical rules)  
✅ **I will use ONLY information from skill files** (no memory/assumptions)  
✅ **I will use `@Model`, not `ViewBag`** (Razor Pages pattern)  
✅ **I will follow UI/CSS design standards** (professional quality)  
✅ **ALL CONTROLS ARE SYNCFUSION** (verified against components.csv, no HTML defaults without confirmation)  
✅ **I will consult skill files during build failures** (mandatory protocol - no guessing)  
✅ **I am ready to generate production code** (confident and prepared)

---

## If This Checklist Has Failures

Do NOT proceed to code generation. Instead:

1. **Identify which section failed** (1-10 above)
2. **Review that section** and complete all checks
3. **Re-read necessary skill files** if knowledge gaps exist
4. **Verify file structure** and naming conventions
5. **Ensure all components have skills** before proceeding
6. **Return to checklist** and re-verify

**A few minutes spent here saves HOURS of debugging build failures.**

---

## During Code Generation

Use this checklist while writing code:

- [ ] Copy tag structure directly from skill files
- [ ] Convert attribute names to camelCase
- [ ] Use `@Model.PropertyName` for all data binding
- [ ] Wrap HTML content in `<e-*-template>`
- [ ] Include all required `@using` statements
- [ ] Follow CSS design standards throughout
- [ ] Verify semantic HTML structure
- [ ] Add accessibility attributes

---

## After Code Generation

Before marking complete:

- [ ] Ran `dotnet build` successfully (no errors)
- [ ] Ran `dotnet run` successfully
- [ ] Page loads without errors in browser
- [ ] Form inputs work (if applicable)
- [ ] Responsive design verified on mobile/tablet/desktop
- [ ] Accessibility verified (keyboard navigation, screen reader)
- [ ] All colors have sufficient contrast
- [ ] Focus states visible on all interactive elements
- [ ] Syncfusion components display correctly
