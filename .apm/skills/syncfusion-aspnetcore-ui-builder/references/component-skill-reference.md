# Component Skill Reference Guide

**How to read component SKILL.md files before code generation.**

---

## Skill File Locations

All component skill files live at:
```
<skill-name>/SKILL.md
```

### Common Components & Skill Paths

| Component | Skill Name | File Path |
|-----------|-----------|-----------|
| Grid | syncfusion-aspnetcore-grid | `syncfusion-aspnetcore-grid/SKILL.md` |
| TextBox/Input | syncfusion-aspnetcore-inputs | `syncfusion-aspnetcore-inputs/SKILL.md` |
| Button | syncfusion-aspnetcore-buttons | `syncfusion-aspnetcore-buttons/SKILL.md` |
| DropDownList | syncfusion-aspnetcore-dropdowns | `syncfusion-aspnetcore-dropdowns/SKILL.md` |
| Chart | syncfusion-aspnetcore-charts | `syncfusion-aspnetcore-charts/SKILL.md` |
| Dialog/Popup | syncfusion-aspnetcore-popups | `syncfusion-aspnetcore-popups/SKILL.md` |

The `skill` field in `component-mapping.json` gives you the exact `<skill-name>`.

---

## Step 1: Extract Components from component-mapping.json

**Parse `component-mapping.json` and identify all unique Syncfusion components and skills.**

Output to display BEFORE reading any skill files:

```
Syncfusion Components: [Grid, TextBox, Button, ...]
Skills to Read:
  - syncfusion-aspnetcore-grid/SKILL.md
  - syncfusion-aspnetcore-inputs/SKILL.md
  - [one line per unique skill]
```

**RULE: SYNCFUSION CONTROLS ONLY** — Do NOT skip, substitute, or use native HTML instead of Syncfusion components.
**If a required Syncfusion component skill is not found → Ask user to confirm before proceeding.**

---

## Step 2: Read SKILL.md for EACH Component Skill

**THIS STEP IS NOT OPTIONAL — Must be completed before writing any code.**

### For EVERY unique skill identified in Step 1:

1. **Read the COMPLETE FILE:** `<skill-name>/SKILL.md`
   - If the file does not exist: **ASK USER CONFIRMATION**
     - Message: *"Component skill not found: `<skill-name>/SKILL.md`. This Syncfusion control requires its skill documentation. Do you want to proceed without this component, or should we install the skill package first? (Y/N)"*
     - If user says NO → Install skill, then continue
     - If user says YES → Proceed without that component (may have limitations)
   - The SKILL.md file is the **ONLY** authoritative source for tag helpers, attributes, and child elements

2. **Extract and record:**
   - **Root tag helper name** (e.g., `<ejs-grid>`, `<ejs-textbox>`)
   - **All child element names** from examples (e.g., `<e-grid-columns>`, `<e-grid-column>`)
   - **Attribute names** used in examples (exact spelling, camelCase)
   - **Required `@using` statements** (e.g., `@using Syncfusion.EJ2`)
   - **Required NuGet package name** (e.g., `Syncfusion.EJ2.AspNet.Core`)
   - **Server-side setup** (PageModel properties, `OnGet` initialization)

3. **Build your skill reference table BEFORE generating code:**

   ```
   [Grid]
     Syncfusion-Only Control: ✅ MUST use <ejs-grid> (never HTML <table>)
     Root tag: <ejs-grid>
     Children: <e-grid-columns>, <e-grid-column>, <e-grid-column-settings>
     Key attrs: dataSource, allowSorting, allowPaging, allowFiltering, height, width
     @using: Syncfusion.EJ2, Syncfusion.EJ2.Grids
     PageModel: 
       - public List<GridData> DataSource { get; set; } = new();
       - Initialize DataSource in OnGet()

   [TextBox]
     Syncfusion-Only Control: ✅ MUST use <ejs-textbox> (never HTML <input>)
     Root tag: <ejs-textbox>
     Children: (none)
     Key attrs: id, name, placeholder, type, floatLabelType, cssClass, required
     @using: Syncfusion.EJ2, Syncfusion.EJ2.Inputs
   
   [Button]
     Syncfusion-Only Control: ✅ MUST use <ejs-button> (never HTML <button>)
     Root tag: <ejs-button>
     Children: (none)
     Key attrs: id, content, type, cssClass, isPrimary, isDisabled
     @using: Syncfusion.EJ2, Syncfusion.EJ2.Buttons
   ```

---

## Step 3: Verify Before Proceeding to Code Generation

**Do NOT proceed if any skill was not read.**

Before writing a single line of `.cshtml`:

- [ ] All skills from component-mapping.json have been identified
- [ ] Read `<skill-name>/SKILL.md` for EVERY skill
- [ ] Confirmed each file existed (did not skip or assume for missing files)
- [ ] Built skill reference table (root tag, children, attributes) for each component
- [ ] Root tag names confirmed from skill files (NOT from memory)
- [ ] Child element names confirmed from skill files (NOT from memory)
- [ ] Attribute names confirmed from skill files (NOT from memory)
- [ ] No attribute or child element will be added that wasn't in the skill file

**If any skill is missing: STOP → Report which skill file is missing.**

---

## Step 4: Generate Code Using ONLY Extracted Information

**Only after completing Steps 1-3:**

- Copy tag structure **exactly** as shown in the skill's SKILL.md
- Substitute model data, IDs, and placeholder values as needed
- Add accessibility attributes (`aria-label`, etc.) around the copied structure
- Do NOT add attributes that were not in the skill examples (unless they are standard HTML attributes)
- Do NOT invent new tag names or attribute names from memory

---

## Common Patterns from Skills

### Enum Resolution in Tag Helpers

When using enums with Syncfusion tag helpers, use the root namespace:

| Enum Type | Required @using | Usage |
|-----------|-----------------|-------|
| DropdownList | `@using Syncfusion.EJ2` | `filterType="Dropdowns.FilterType.Contains"` |
| Charts | `@using Syncfusion.EJ2` | `valueType="Charts.ValueType.Category"` |
| Scheduler | `@using Syncfusion.EJ2` | Reference as `Schedule.ViewType.Week` |
| Grid | `@using Syncfusion.EJ2` | Reference as `Grid.SortDirection.Ascending` |

**CORRECT:**
```razor
@using Syncfusion.EJ2
<ejs-dropdownlist filterType="Dropdowns.FilterType.Contains"></ejs-dropdownlist>
```

**INCORRECT - Do NOT do this:**
```razor
@using Syncfusion.EJ2.Dropdowns
filterType="FilterType.Contains"  @* Will cause "does not exist" errors *@
```

---

## Example: Reading a Skill File

**Your reference table after reading `syncfusion-aspnetcore-grid/SKILL.md`:**

```
Component: Grid

Root Tag: <ejs-grid>

Children:
  <e-grid-columns>
    <e-grid-column>

Child Configuration:
  <e-grid-column-settings>
  <e-grid-column-field>

Supported Attributes on <ejs-grid>:
  - dataSource: IEnumerable<T>
  - allowSorting: bool
  - allowPaging: bool
  - allowFiltering: bool
  - allowSelection: bool
  - selectionSettings: <e-grid-selectionsettings>
  - allowResizing: bool
  - allowReordering: bool
  - height: string (e.g., "400px")
  - width: string (e.g., "100%")
  - pageSettings: <e-grid-pagesettings>

Supported Attributes on <e-grid-column>:
  - field: string (e.g., "OrderID")
  - headerText: string
  - width: string
  - type: string ("text", "date", "datetime", "number", "checkbox", "dropdown")
  - format: string (e.g., "yMd" for dates)
  - textAlign: string ("Left", "Right", "Center")
  - visible: bool
  - allowSorting: bool
  - allowFiltering: bool
  - isPrimaryKey: bool

Supported Attributes on <e-grid-pagesettings>:
  - pageSize: int
  - pageCount: int
  - currentPage: int

PageModel Setup:
  public List<OrderData> Orders { get; set; } = new();

  public void OnGet() {
      Orders = GetOrders(); // Populate from database
  }

@using Statements Required:
  @using Syncfusion.EJ2
  @using Syncfusion.EJ2.Grids

Razor Page Example:
  @page
  @using Syncfusion.EJ2
  @using Syncfusion.EJ2.Grids
  @model GridPageModel

  <ejs-grid dataSource="@Model.Orders" 
            allowPaging="true" 
            allowSorting="true">
    <e-grid-pagesettings pageSize="10"></e-grid-pagesettings>
    <e-grid-columns>
      <e-grid-column field="OrderID" headerText="Order ID" width="100"></e-grid-column>
      <e-grid-column field="CustomerName" headerText="Customer Name" width="120"></e-grid-column>
    </e-grid-columns>
  </ejs-grid>
```

---

## What NOT to Do

❌ **DO NOT** guess tag names or attributes from AI training knowledge  
❌ **DO NOT** assume syntax that isn't explicitly shown in the SKILL.md file  
❌ **DO NOT** use native HTML instead of Syncfusion components (this is REQUIRED)
   - ❌ Never: `<input type="text">` → ✅ Always: `<ejs-textbox>`
   - ❌ Never: `<table>` → ✅ Always: `<ejs-grid>`
   - ❌ Never: `<button>` → ✅ Always: `<ejs-button>`
❌ **DO NOT** invent child element names  
❌ **DO NOT** use different attribute casing than shown in examples  
❌ **DO NOT** skip reading any skill file  
❌ **DO NOT** substitute missing skills with native HTML — ask user for confirmation instead  

---

## When a Skill File Is Missing

If `<skill-name>/SKILL.md` does not exist:

1. **ASK USER CONFIRMATION:**
   ```
   ⚠️  Skill file not found: '<skill-name>/SKILL.md'
   
   This Syncfusion ASP.NET Core control requires its skill documentation.
   
   Options:
   (A) Continue WITHOUT this component (may limit functionality)
   (B) Wait for me to guide you installing the skill package
   
   Choose A or B:
   ```

2. **If user chooses A:** Proceed with code generation but skip that component
3. **If user chooses B:** Provide install instructions and retry
4. **NEVER substitute with native HTML** — Syncfusion controls are required, not optional
5. **RULE:** All controls must be Syncfusion ASP.NET Core components only

---

## Checklist Before Code Generation

- [ ] All unique skills identified from component-mapping.json
- [ ] All skill files located and confirmed to exist
- [ ] All skill files completely read (not skimmed)
- [ ] Skill reference table built for each component
- [ ] No missing skill files (would have been reported and stopped)
- [ ] Ready to generate code using extracted information ONLY
