# Tag Helper Syntax Rules (CRITICAL — PREVENTS BUILD ERRORS)

**These 6 universal rules apply to ANY Syncfusion ASP.NET Core control. Violating any causes RZ2010 or CS0117 compile errors.**

---

## Rule 1: Tag Names - NO Hyphens Between Words (Except First)

**Formula:** `<e-[component]-[descriptor-no-hyphens]>`

**WRONG** - Causes RZ2010 "tag is not allowed by parent"
```razor
<e-[component]-[word]-[word]-[settings]>     @* Multiple hyphens in descriptor *@
<e-[component]-[entity]-[field]>             @* Hyphens in descriptor portion *@
<e-[component]-[word]-[word]>                @* Generic example - hyphen in middle *@
```

**CORRECT** - Join all descriptor words, no hyphens
```razor
<e-[component]-[word][word][settings]>       @* Correct - no hyphens in descriptor *@
<e-[component]-[entity][field]>              @* Correct - joined together *@
<e-[component]-[word][word]>                 @* Correct - concatenated *@
```

**Key:** Remove ALL hyphens EXCEPT the first one (which separates component from descriptor).

---

## Rule 2: Nested Tags - Always Use Parent-Prefixed Child Elements

**Formula:** `<ejs-component><e-component-child>...</e-component-child></ejs-component>`

**WRONG** - Child without parent prefix
```razor
<ejs-component>
    <e-child>...</e-child>                   @* Wrong - missing parent prefix *@
    <e-item>...</e-item>                     @* Wrong - bare name *@
    <div>Content</div>                       @* Wrong - HTML not allowed here *@
</ejs-component>
```

**CORRECT** - Child includes parent name as prefix
```razor
<ejs-component>
    <e-component-child>...</e-component-child>     @* Correct - has parent prefix *@
    <e-component-items>                           @* Correct - collection pattern *@
        <e-component-item>...</e-component-item>  @* Correct - prefixed *@
    </e-component-items>
    <e-content-template>                          @* Correct - special template tag *@
        <div>Content</div>                        @* Correct - content inside template *@
    </e-content-template>
</ejs-component>
```

**Key:** Every child element MUST start with `<e-[parent-name]-...>`. Parent name comes from `<ejs-[name]>`.

---

## Rule 3: Attributes - Convert ALL Hyphens to CamelCase

**Formula:** `[word]-[word]` → `[word][Word]` (capitalize next word)

**WRONG** - Hyphenated attribute names
```razor
<ejs-component attribute-name="value"
               another-long-attribute="value"
               is-something="true"
               allow-feature="true">
```

**CORRECT** - CamelCase attribute names
```razor
<ejs-component attributeName="value"
               anotherLongAttribute="value"
               isSomething="true"
               allowFeature="true">
```

**Key:** For every hyphen in an attribute name, capitalize the next word and remove the hyphen.

---

## Rule 4: Content Wrappers - Always Use Template Tags

**Formula:** If element contains HTML content → wrap in `<e-[element]-template>`

**WRONG** - Direct HTML content in elements
```razor
<ejs-dialog>
    <div>Content here</div>                  @* Wrong - not in template *@
</ejs-dialog>

<e-component-item>
    <span>Some text</span>                   @* Wrong - HTML without wrapper *@
</e-component-item>
```

**CORRECT** - HTML wrapped in template element
```razor
<ejs-dialog>
    <e-content-template>
        <div>Content here</div>              @* Correct - in template *@
    </e-content-template>
</ejs-dialog>

<e-component-item>
    <e-content-template>
        <span>Some text</span>               @* Correct - wrapped in template *@
    </e-content-template>
</e-component-item>
```

**Key:** Any HTML/markup inside a tag element MUST be wrapped in `<e-*-template>`.

---

## Rule 5: Data Binding - Use @Model, NOT ViewBag

**Razor Pages Pattern:** Always use `@Model.PropertyName` for data binding.

**WRONG** - ViewBag usage in Razor Pages
```csharp
// PageModel
public void OnGet() {
    ViewBag.DataSource = GetData();  @* Wrong - ViewBag is for MVC *@
}
```

```razor
<ejs-component dataSource="@ViewBag.DataSource">  @* Wrong - ViewBag *@
```

**CORRECT** - Model properties in Razor Pages
```csharp
// PageModel
public List<Item> DataSource { get; set; } = new();

public void OnGet() {
    DataSource = GetData();  @* Correct - public property *@
}
```

```razor
<ejs-component dataSource="@Model.DataSource">  @* Correct - @Model *@
```

**Key:** Razor Pages = PageModel properties (`@Model`). Razor MVC = ViewBag. Use the correct one.

---

## Rule 6: Unsupported Nested Configuration Tags

**Pattern:** Some nested tags like `<e-*-events>` are NOT supported. Use attributes instead.

**WRONG** - Unsupported configuration tags
```razor
<ejs-component>
    <e-component-events />                   @* NOT supported *@
    <e-component-contextmenuitems>           @* NOT supported *@
    <e-component-toolbaritems>               @* NOT supported *@
</ejs-component>
```

**CORRECT** - Use attribute-based configuration
```razor
<ejs-component eventName="@Model.Handler"
               allowContextMenu="true"
               toolbar="@Model.ToolbarItems">
    @* Configuration via attributes, not nested tags *@
</ejs-component>
```

**Key:** Check the component's `SKILL.md`. If nested configuration isn't shown there, it's not supported. Use the attribute approach instead.

---

## Quick Reference Table

| Scenario | Pattern |
|----------|---------|
| **Tag names** | `<e-[component]-[no-hyphens-here]>` |
| **Child tags** | `<e-[parent]-[child]>` inside `<ejs-[parent]>` |
| **Attributes** | `attributeName="value"` (camelCase, no hyphens) |
| **Content** | Wrap in `<e-*-template>` before adding HTML |
| **Data** | Use `@Model.Property` (Razor Pages) |
| **Config** | Use attributes, not nested `<e-*-events>` tags |

---

## How to Avoid Build Failures

Before generating code, memorize these 6 rules and verify:

1. ✅ Tag names have hyphens ONLY between component and descriptor
2. ✅ All child tags start with `<e-[parent-name]-...>`
3. ✅ All attributes use camelCase (no hyphens)
4. ✅ All HTML content wrapped in `<e-*-template>`
5. ✅ Data binding uses `@Model`, not `ViewBag`
6. ✅ No unsupported nested configuration tags (use attributes instead)

**If ANY rule is violated → build fails. Check the skill file's SKILL.md to confirm syntax.**
