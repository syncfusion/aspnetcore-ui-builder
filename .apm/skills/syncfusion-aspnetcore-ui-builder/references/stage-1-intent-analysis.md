# Stage 1: Intent Analysis

**Purpose:** Parse and validate the user's natural language request, identify component type and modifiers, resolve ambiguities.

**AI Should:**
- Read the user's raw query carefully
- Identify primary intent: `generate_page`, `generate_partial`, or `modify_existing`
- Extract component type (e.g., "login page" → page/login, "data grid page" → page/data-grid)
- Extract modifiers (e.g., "dark theme" → styling:dark, "with filtering" → feature:filtering)
- Identify target directory if specified (e.g., "in the Pages/Auth folder" → targetDir:Pages/Auth/)
- Identify Razor Pages specific requirements (e.g., PageModel needed, tag helpers required)

**Ambiguity Resolution:**
If the request is unclear, ask ONE clarifying question. Examples:

| Ambiguous Input | Clarifying Question |
|---|---|
| "Build me a page with a form" | "What kind of form? (login, registration, contact, multi-step)" |
| "Add a grid to my page" | "What grid features do you need? (sorting, filtering, paging, editing)" |
| "Make the dashboard better" | "Which aspect needs improvement? (accessibility, styling, data binding)" |

**Output to User:**
One-line confirmation:
```
✓ Understood: Generating a dark-themed DataGrid page with sorting and filtering.
Starting project detection...
```

**Status:** This stage requires NO user interaction for confirmation. AI decides intent based on pure reasoning.
