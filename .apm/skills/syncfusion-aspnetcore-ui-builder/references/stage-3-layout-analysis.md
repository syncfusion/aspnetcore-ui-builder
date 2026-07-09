# Stage 3: Layout Analysis & Component Mapping (Combined)

**Purpose:** Analyze user requirements, create optimal component-mapping.json, and map to Syncfusion components automatically. **FULLY AUTOMATED — NO user interaction.**

---

## Stage 3: Layout Analysis

### AI Should:

1. **Read component type** from Stage 1 intent analysis
2. **Analyze user query** for specific requirements and context
3. **Determine optimal layout variant** (no user choice needed)
4. **Create structured component-mapping.json** with all elements
5. **Output JSON** for Stage 3-4 combined processing

### Decision Framework

Based on user requirements, AI selects the **best** layout (not multiple options):

| Component Type | Decision Criteria | Best Variant |
|---|---|---|
| **Login Page** | Enterprise? 2FA needed? Social login? | Choose: Minimal/Standard/Advanced |
| **Data Grid Page** | Read-only or editable? Export needed? | Choose: Simple/Interactive/Full-featured |
| **Dashboard Page** | Internal or customer-facing? Complexity? | Choose: Focused/Standard/Enterprise |
| **Form Page** | Single-step or multi-step? Validation level? | Choose: Basic/Standard/Advanced |

**Key Principle:** AI makes the optimal choice based on the user query context and best practices. No variant selection UI needed.

### Output: Structured JSON (for Stage 3-4 Component Mapping)

```json
{
  "component_type": "Login Page",
  "variant": "Standard",
  "elements": [
    {
      "id": "email_input",
      "name": "Email Address",
      "description": "Email field with validation",
      "type_hint": "text input email form validation"
    },
    {
      "id": "password_input",
      "name": "Password",
      "description": "Password field, masked",
      "type_hint": "text input password form masked"
    },
    {
      "id": "remember_me",
      "name": "Remember Me",
      "description": "Keep me logged in",
      "type_hint": "checkbox form input"
    },
    {
      "id": "submit_button",
      "name": "Submit",
      "description": "Login button",
      "type_hint": "button primary action submit cta"
    }
  ],
  "icon_elements": [
    {
      "id": "forgot_password_link",
      "name": "Forgot Password",
      "description": "Password reset link",
      "type": "link",
      "icon_hint": "help question info reset"
    },
    {
      "id": "error_message",
      "name": "Error",
      "description": "Error indicator",
      "type": "icon",
      "icon_hint": "error warning alert"
    }
  ]
}
```

**JSON Structure Details:**

- `component_type`: The page being built (e.g., "Login Page", "Data Grid Page", "Dashboard Page")
- `variant`: Chosen variant based on user requirements (e.g., "Standard", "Advanced", "Minimal")
- `sections` (optional): For complex layouts, group elements into logical sections
  - `section_id`: Unique identifier (e.g., "header_section")
  - `section_name`: Display name (e.g., "Header")
  - `elements`: Array of elements within section
- `elements`: Array of component elements
  - `id`: Unique identifier (snake_case)
  - `name`: Display name for UI
  - `description`: What this element does
  - `type_hint`: UI element type for search (e.g., "text input", "button", "dropdown", "grid", "chart")

**Important:**
- `type_hint` is critical for component mapping accuracy
- Keep descriptions concise and functional
- Use lowercase for `id` and `type_hint`
- Create `component-mapping.json` in project root (reused in Stage 4 & 5)
- Output minimal summary table in chat for visibility

### Type Hint Best Practices

**For Header/AppBar Elements:**
- Always include `appbar` or `header` keyword in type_hint
- Examples:
  - Logo: `"image logo appbar header branding"`
  - Notifications: `"icon button notification appbar header"`
  - User Menu: `"dropdown button menu user profile appbar header"`

**General Guidelines:**
- Use **compound keywords** - `"icon button notification"` scores better than `"notification"`
- Include **context keywords** - appbar/header/sidebar context improves matching
- Add **modifiers** - sortable, filterable, collapsible, paginated

---

## Complex Layouts (Multi-Section)

For dashboards, admin panels, or multi-section pages:

```json
{
  "component_type": "Admin Dashboard Page",
  "variant": "Classic Admin Dashboard",
  "layout_grid": "2-column",
  "sections": [
    {
      "section_id": "header",
      "section_name": "Header",
      "description": "Fixed top navigation",
      "responsive": "fixed",
      "elements": [
        {
          "id": "logo",
          "name": "Company Logo",
          "description": "Brand logo in app bar",
          "type_hint": "image logo appbar header branding"
        },
        {
          "id": "notification_bell",
          "name": "Notifications",
          "description": "Bell icon with count in header",
          "type_hint": "icon button notification appbar header"
        },
        {
          "id": "user_menu",
          "name": "User Profile",
          "description": "User avatar dropdown menu",
          "type_hint": "dropdown button menu user profile appbar header"
        }
      ]
    },
    {
      "section_id": "sidebar",
      "section_name": "Sidebar",
      "description": "Left navigation",
      "responsive": "collapsible",
      "elements": [
        {
          "id": "nav_menu",
          "name": "Navigation Menu",
          "description": "Main navigation",
          "type_hint": "sidebar navigation collapsible"
        }
      ]
    },
    {
      "section_id": "main_content",
      "section_name": "Main Content",
      "responsive": "flexible",
      "elements": [
        {
          "id": "kpi_cards",
          "name": "KPI Cards",
          "description": "Metric cards displaying statistics",
          "type_hint": "card grid statistics dashboard metrics kpi"
        },
        {
          "id": "data_grid",
          "name": "Users Grid",
          "description": "Data grid with sorting and filtering",
          "type_hint": "grid data grid table sortable filterable paging"
        }
      ]
    }
  ]
}
```

---

## Stage 3-4 File-Based Workflow (TOKEN OPTIMIZATION)

### ⚠️ MANDATORY: Create component-mapping.json in Project Root

**Step 1: Create `component-mapping.json`** in project root
**Step 2: Map elements to Syncfusion Razor tag helpers**
**Step 3: Capture mapping in chat context**

### Component Mapping for Razor Pages

Syncfusion components in Razor Pages use **tag helpers** with `e-` prefix:

| Element Type | Syncfusion Tag Helper |
|--------------|----------------------|
| Text Input | `<ejs-textbox>` |
| Password Input | `<ejs-textbox>` with `type="password"` |
| Checkbox | `<ejs-checkbox>` |
| Button | `<ejs-button>` |
| Data Grid | `<ejs-grid>` |
| Dropdown | `<ejs-dropdownlist>` |
| DatePicker | `<ejs-datepicker>` |
| Dialog | `<ejs-dialog>` |
| Tabs | `<ejs-tab>` |
| Card | `<ejs-card>` |

### Output: Component Mapping

```json
{
  "component_type": "Login Page",
  "variant": "Standard",
  "mapped_components": [
    {
      "element_id": "email_input",
      "element_name": "Email Address",
      "tag_helper": "ejs-textbox",
      "skill": "syncfusion-aspnetcore-inputs",
      "attributes": {
        "id": "email",
        "name": "email",
        "type": "email",
        "placeholder": "Enter email"
      }
    },
    {
      "element_id": "password_input",
      "element_name": "Password",
      "tag_helper": "ejs-textbox",
      "skill": "syncfusion-aspnetcore-inputs",
      "attributes": {
        "id": "password",
        "name": "password",
        "type": "password",
        "placeholder": "Enter password"
      }
    },
    {
      "element_id": "remember_me",
      "element_name": "Remember Me",
      "tag_helper": "ejs-checkbox",
      "skill": "syncfusion-aspnetcore-buttons",
      "attributes": {
        "id": "rememberMe",
        "label": "Remember Me"
      }
    },
    {
      "element_id": "submit_button",
      "element_name": "Submit",
      "tag_helper": "ejs-button",
      "skill": "syncfusion-aspnetcore-buttons",
      "attributes": {
        "id": "submitBtn",
        "content": "Login",
        "type": "submit"
      }
    }
  ]
}
```

---

## Mandatory Post-Mapping: Skill File Verification

**After running `components-search.cjs` and writing `component-mapping.json`, you MUST:**

1. **Extract all unique `skill` values** from the mapped `component-mapping.json`
2. **Verify each skill file exists** at `<skill-name>/SKILL.md`
3. **Report any missing skill files** before proceeding to Stage 4/5:
   ```
   ✅ syncfusion-aspnetcore-grid/SKILL.md — FOUND
   ✅ syncfusion-aspnetcore-inputs/SKILL.md — FOUND
   ❌ syncfusion-aspnetcore-charts/SKILL.md — MISSING
   ```
4. **If any skill file is missing:** Ask user confirmation — *"Skill `<skill-name>/SKILL.md` not found. Continue without this component (A) or wait for install instructions (B)?"* Do NOT hard-stop; let user decide.

**⛔ CRITICAL:** All code generation uses Syncfusion controls ONLY — no native HTML substitutes allowed.

---

## Status

✅ **FULLY AUTOMATED** - No user interaction
✅ **Single pass** - component-mapping.json created once, components mapped immediately
✅ **Token efficient** - No duplication or variant selection overhead
✅ **Razor-focused** - Tag helpers for ASP.NET Core Razor Pages
✅ **Ready for Stage 5** - Component mapping feeds directly to code generation
✅ **Skill files verified** - All component skills confirmed present before code generation

---

## Architecture

- **Input**: User requirements + component type from Stage 1
- **Processing**: 
  - Component analysis → JSON structure with `type_hint`
  - Tag helper mapping for Razor Pages
- **Output**: 
  - `component-mapping.json` (project root) - layout structure for Stage 4 & 5
  - Chat summary table - element count, tag helpers mapped
   "Syncfusion Components Selected: [name1], [name2], [name3]"
- **Context**: Component mapping results kept in conversation (no file artifact beyond component-mapping.json)
