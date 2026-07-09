# Code Generation Workflow

**Complete process for generating production-ready Razor pages with Syncfusion components.**

---

## Overview

After reading all component skills (see [component-skill-reference.md](component-skill-reference.md)), follow this workflow:

1. **Generate Razor Page (.cshtml)** with tag helpers (uses _Layout.cshtml)
2. **Generate PageModel (.cs)** with properties and handlers
3. **Generate Professional CSS (.css)** following design standards
4. **Verify all files** against pre-generation checklist

**⭐ CRITICAL PREREQUISITE:** Pages/Shared/_Layout.cshtml must have:
- Theme CSS link in `<head>` section
- Syncfusion JS script in `<head>` section (after theme CSS)
- `<ejs-scripts></ejs-scripts>` tag before `</body>` closing tag (CRITICAL for tag helpers)
- `@addTagHelper *, Syncfusion.EJ2` in _ViewImports.cshtml

---

## Phase 1: Generate Razor Page (.cshtml)

## Phase 1: Generate Razor Page (.cshtml)

### Basic Structure (Uses Shared _Layout.cshtml)

```razor
@page
@using Syncfusion.EJ2
@using Syncfusion.EJ2.Dropdowns
@using Syncfusion.EJ2.Grids
@using Syncfusion.EJ2.Charts
@model PageNameModel

<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Page Title</title>
    <!-- ⭐ Page-specific CSS only (theme CSS in _Layout.cshtml) -->
    <link rel="stylesheet" href="~/css/page-styles.css">
</head>
<body>
    <main class="page-container" role="main">
        <header class="page-header">
            <h1>Page Title</h1>
        </header>
        
        <section class="page-content">
            <!-- Syncfusion components using tag helpers -->
            <ejs-textbox id="email" name="Email" placeholder="Enter email"></ejs-textbox>
            <ejs-button id="submit" content="Submit" type="submit"></ejs-button>
        </section>
        
        <footer class="page-footer">
            <!-- Footer info -->
        </footer>
    </main>
    
    <!-- ⚠️ DO NOT add theme CSS or Syncfusion scripts here - they're in _Layout.cshtml -->
    <!-- ⚠️ NEVER add <ejs-scripts> here - must be in _Layout.cshtml only -->
</body>
</html>
```

**⭐ CRITICAL REQUIREMENTS:**
- ✅ Theme CSS in `Pages/Shared/_Layout.cshtml` `<head>` section
- ✅ Syncfusion JS in `Pages/Shared/_Layout.cshtml` `<head>` section (after theme CSS)
- ✅ `<ejs-scripts></ejs-scripts>` in `Pages/Shared/_Layout.cshtml` before `</body>` closing tag
- ✅ Page-specific CSS can be added to individual pages
- ✅ Tag helpers work because _Layout.cshtml has `<ejs-scripts></ejs-scripts>`

### Important: Enum Resolution in Tag Helpers

When using enums with Syncfusion tag helpers, use the root namespace:

**CORRECT - Always use base `@using Syncfusion.EJ2`:**
```razor
@using Syncfusion.EJ2
<ejs-dropdownlist filterType="Dropdowns.FilterType.Contains"></ejs-dropdownlist>
<ejs-chart valueType="Charts.ValueType.Category"></ejs-chart>
```

**INCORRECT - Do NOT do this:**
```razor
@using Syncfusion.EJ2.Dropdowns  @* This causes "does not exist" errors *@
filterType="FilterType.Contains"  @* Missing namespace prefix *@
```

| Enum Type | Required @using | Example |
|-----------|-----------------|---------|
| DropdownList filters | `@using Syncfusion.EJ2` | `filterType="Dropdowns.FilterType.Contains"` |
| Charts enums | `@using Syncfusion.EJ2` | `valueType="Charts.ValueType.Category"` |
| Scheduler enums | `@using Syncfusion.EJ2` | `viewType="Schedule.ViewType.Week"` |
| Grid enums | `@using Syncfusion.EJ2` | `sortDirection="Grid.SortDirection.Ascending"` |

---

## Phase 2: Generate PageModel (.cs)

### Basic Structure

```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.RazorPages;
using System.Collections.Generic;

namespace YourNamespace.Pages
{
    public class PageNameModel : PageModel
    {
        // Properties for data binding
        [BindProperty]
        public string Email { get; set; }

        public List<GridData> DataSource { get; set; } = new();

        // GET handler
        public void OnGet()
        {
            // Initialize page data
            LoadData();
        }

        // POST handler
        public IActionResult OnPost()
        {
            if (!ModelState.IsValid)
            {
                return Page();
            }

            // Handle form submission
            ProcessFormData();

            return RedirectToPage("Success");
        }

        private void LoadData()
        {
            // Populate DataSource from database or service
            DataSource = new List<GridData>
            {
                new GridData { Id = 1, Name = "Item 1" },
                new GridData { Id = 2, Name = "Item 2" }
            };
        }

        private void ProcessFormData()
        {
            // Process form data
        }
    }

    public class GridData
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }
}
```

### PageModel Requirements

- ✅ Inherit from `PageModel`
- ✅ Use `[BindProperty]` for form inputs
- ✅ Create public properties for `@Model` binding
- ✅ Implement `OnGet()` and `OnPost()` handlers
- ✅ Use async handlers when needed: `OnGetAsync()`, `OnPostAsync()`
- ✅ Initialize collections (lists, etc.) in `OnGet()`
- ✅ Include data model classes in same file or separate file

---

## Phase 3: Generate Professional CSS

### Step 1: Start with CSS Variables

```css
/* ========================================
   Page Styles: [PageName]
   ======================================== */

:root {
  --primary-color: #0066cc;
  --primary-dark: #0052a3;
  --primary-light: #e6f0ff;
  
  --text-primary: #333333;
  --text-secondary: #666666;
  --text-tertiary: #999999;
  --background: #ffffff;
  --border: #d0d0d0;
  
  --success: #28a745;
  --error: #dc3545;
  --warning: #ffc107;
  --info: #17a2b8;
  
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;
  --spacing-2xl: 3rem;
  
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
}
```

### Step 2: Page Layout

```css
/* Page Container */
.page-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: var(--spacing-2xl);
  background: var(--background);
}

.page-header {
  margin-bottom: var(--spacing-2xl);
  padding-bottom: var(--spacing-lg);
  border-bottom: 1px solid var(--border);
}

.page-header h1 {
  font-size: 2rem;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0;
}

.page-content {
  margin-bottom: var(--spacing-2xl);
}

.page-footer {
  margin-top: var(--spacing-2xl);
  padding-top: var(--spacing-lg);
  border-top: 1px solid var(--border);
  font-size: 0.875rem;
  color: var(--text-secondary);
  text-align: center;
}
```

### Step 3: Responsive Design (Mobile-First)

```css
/* Mobile (base): 320px+ */
.page-container {
    padding: var(--spacing-md);
}

.page-header h1 {
    font-size: 1.5rem;
}

/* Tablet: 640px+ */
@media (min-width: 640px) {
    .page-container {
        padding: var(--spacing-lg);
    }
    
    .page-header h1 {
        font-size: 1.75rem;
    }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
    .page-container {
        padding: var(--spacing-xl);
    }
    
    .page-header h1 {
        font-size: 2rem;
    }
}

/* Wide: 1280px+ */
@media (min-width: 1280px) {
    .page-container {
        max-width: 1400px;
    }
}
```

### Step 4: Component-Specific Styles

```css
/* Form Components */
.form-container {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
}

.form-group {
    display: flex;
    flex-direction: column;
}

.form-label {
    font-weight: 600;
    color: var(--text-primary);
    margin-bottom: var(--spacing-sm);
    font-size: 0.95rem;
}

.form-input {
    border: 1px solid var(--border);
    border-radius: var(--radius-md);
    padding: var(--spacing-md);
    font-size: 1rem;
    transition: border-color 0.3s, box-shadow 0.3s;
}

.form-input:focus {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px var(--primary-light);
    outline: none;
}

/* Buttons */
.btn {
    padding: var(--spacing-md) var(--spacing-lg);
    border: none;
    border-radius: var(--radius-md);
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    min-height: 44px;
}

.btn-primary {
    background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
    color: white;
}

.btn-primary:hover {
    box-shadow: 0 4px 12px rgba(0, 102, 204, 0.3);
    transform: translateY(-2px);
}

.btn-primary:active {
    transform: translateY(0);
}

/* Syncfusion Component Overrides */
.e-textbox, .e-input-group {
    border-radius: var(--radius-md);
}

.e-input-group:focus-within {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px var(--primary-light);
}

.e-grid {
    background: var(--background);
    border-radius: var(--radius-lg);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.e-gridheader {
    background: #f5f5f5;
    font-weight: 600;
}

.e-gridcontent .e-row:hover {
    background: #f9f9f9;
}
```

### CSS Generation Checklist

**Core Styles:**
- [ ] CSS variables defined for colors, spacing, radius
- [ ] Mobile-first approach (base styles, then expand)
- [ ] Media queries at 640px, 1024px, 1280px breakpoints
- [ ] 4.5:1 color contrast minimum (WCAG AA)
- [ ] Interactive elements ≥ 44x44px (touch friendly)
- [ ] 8px spacing system used throughout
- [ ] Smooth transitions (0.3s typical)
- [ ] Focus states visible and accessible
- [ ] Flexbox/Grid for layouts (no fixed widths)
- [ ] Semantic HTML styling (h1, form, button)
- [ ] Syncfusion component customization
- [ ] Print styles (if needed)

**UI Glitch Prevention** (from `ui-css-design-standards.md` sections 7-12):
- [ ] Text truncation: `.truncate-single` (ellipsis), `.truncate-lines` (multi-line)
- [ ] Text wrapping: `.text-wrap-safe` prevents overflow and overlap
- [ ] Log/code text: `.log-text` with `white-space: pre-wrap` and `word-break`
- [ ] Tree/list labels: `.tree-item-text` visible and not clipped
- [ ] Table cells: `min-width: 0` for proper flex truncation
- [ ] Image sizing: `max-width: 100%`, `object-fit` for aspect ratio
- [ ] Modal images: `.modal-image` with `object-fit: contain`
- [ ] Card images: `.card-image` with `object-fit: cover`
- [ ] Appointment spacing: flex layout with `gap` prevents time/status overlap
- [ ] Grid cells: proper padding and `min-width: 0` to prevent text collision
- [ ] Card titles/descriptions: multi-line truncation with `-webkit-line-clamp`
- [ ] Modal content: proper height handling with `min-height: 0` for scrolling
- [ ] Responsive overflow: mobile adjustments for `font-size` and `padding`

---

## Phase 4: Verification

Before considering code generation complete:

**HTML/Razor Page:**
- [ ] All `@using` statements for required namespaces
- [ ] All tag helpers follow syntax rules from [tag-helper-syntax-rules.md](tag-helper-syntax-rules.md)
- [ ] All data binding uses `@Model` (not `ViewBag`)
- [ ] Semantic HTML structure (`<main>`, `<header>`, `<section>`, `<footer>`)
- [ ] Accessibility attributes (`role`, `aria-label`, etc.)

**PageModel (.cs):**
- [ ] Inherits from `PageModel`
- [ ] All form inputs marked with `[BindProperty]`
- [ ] Data properties initialized (e.g., `= new()`)
- [ ] OnGet() and OnPost() handlers implemented
- [ ] Data model classes defined
- [ ] Using statements correct

**CSS:**
- [ ] CSS variables for theme integration
- [ ] Mobile-first responsive design
- [ ] Color contrast meets WCAG AA
- [ ] Touch-friendly interactive elements
- [ ] 8px spacing system
- [ ] Professional styling throughout
- [ ] Syncfusion component overrides

---

## Common Patterns

### Grid with Data Binding

**Razor Page:**
```razor
<ejs-grid dataSource="@Model.Items" allowPaging="true" allowSorting="true">
    <e-grid-pagesettings pageSize="10"></e-grid-pagesettings>
    <e-grid-columns>
        <e-grid-column field="Id" headerText="ID" width="50"></e-grid-column>
        <e-grid-column field="Name" headerText="Name" width="100"></e-grid-column>
    </e-grid-columns>
</ejs-grid>
```

**PageModel:**
```csharp
public List<Item> Items { get; set; } = new();

public void OnGet()
{
    Items = GetItemsFromDatabase();
}
```

### Form with Validation

**Razor Page:**
```razor
<form method="post" class="form-container">
    <div class="form-group">
        <label for="email">Email</label>
        <ejs-textbox id="email" name="Email" type="email" required></ejs-textbox>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

**PageModel:**
```csharp
[BindProperty]
[Required]
[EmailAddress]
public string Email { get; set; }

public IActionResult OnPost()
{
    if (!ModelState.IsValid)
        return Page();
    
    // Process valid form
    return Page();
}
```

---

## Next Steps After Code Generation

1. **Build the project** to verify no syntax errors:
   ```bash
   dotnet build
   ```

2. **Run the application:**
   ```bash
   dotnet run
   ```

3. **Test the page** in browser:
   - Verify layout and styling
   - Test form inputs and interactions
   - Check responsive design on mobile
   - Verify accessibility (keyboard navigation, screen readers)

4. **Fix any errors:**
   - Compiler errors: Check tag helper syntax against skill files
   - Runtime errors: Check PageModel properties and initialization
   - Styling issues: Verify CSS variables and responsive breakpoints

---

## Files Generated

For a page named "Products":
- `Pages/Products/Index.cshtml` - Razor page with UI
- `Pages/Products/Index.cshtml.cs` - PageModel with logic
- `wwwroot/css/products.css` - Professional styling

All three files must be present and correctly structured for the page to function.
