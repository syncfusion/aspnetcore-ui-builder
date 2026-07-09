# Validation Rules Reference

**Purpose:** Comprehensive checklist for Stage 7 validation. Used to validate Razor Pages component against web standards.

## Binary Validation Result

Each component receives a **PASS ✓** or **FAIL ✗** result against these rules.

---

## Accessibility (WCAG 2.1 AA) - Blocking

| Rule | Check | Pass/Fail |
|------|-------|-----------|
| **Semantic HTML** | All form elements use proper tag helpers (`<form>`, `<label>`, `<input>`, `<button>`) | |
| **ARIA Labels** | Form inputs have `aria-label` or associated `<label>` | |
| **ARIA Errors** | Invalid inputs have `aria-invalid="true"` + error message | |
| **Focus Indicator** | All interactive elements have visible focus outline | |
| **Keyboard Nav** | Tab order follows visual flow, no keyboard traps | |
| **Color Contrast** | Text ≥ 4.5:1, focus indicator ≥ 3:1 contrast | |
| **Touch Targets** | Interactive elements ≥ 44x44px | |

---

## Security - Blocking

| Rule | Check | Pass/Fail |
|------|-------|-----------|
| **No XSS** | No `Html.Raw()` or inline event handlers in Razor | |
| **Antiforgery Token** | Forms use `@Html.AntiForgeryToken()` | |
| **Input Validation** | User input validated via model binding and `[BindProperty]` | |
| **No Secrets** | No hardcoded API keys, JWT, or database URLs | |
| **Syncfusion License** | License key in environment variable, not hardcoded | |

---

## Performance - Warning (Auto-fixable)

| Rule | Check | Status |
|------|-------|--------|
| **ViewData/TempData** | Heavy data passed via ViewBag/TempData appropriately | ⚠️ Can warn |
| **Async Operations** | Database/network calls use async/await | ⚠️ Can auto-fix |
| **Bundle Size** | No unnecessary script includes or large libraries | ⚠️ Can warn |

---

## Responsive Design - Warning (Auto-fixable)

| Rule | Check | Status |
|------|-------|--------|
| **Mobile-First** | CSS starts mobile (320px), then expands | ⚠️ Can auto-fix |
| **Flexbox/Grid** | No fixed widths, uses responsive layouts | ⚠️ Can auto-fix |
| **Media Queries** | Breakpoints at 320px, 768px, 1024px | ⚠️ Can auto-fix |

---

## Code Quality - Warning

| Rule | Check | Status |
|------|-------|--------|
| **C# Types** | Strong typing with ViewModel/PageModel classes | ⚠️ Can auto-fix |
| **XML Comments** | Complex methods documented with `///` comments | ⚠️ Can add |
| **Error Handling** | Try-catch on async operations, user-friendly messages | ⚠️ Can auto-fix |

---

## Validation Logic (Stage 7)

### Step 1: Check Blocking Rules
If ANY blocking rule fails → **FAIL ✗**
- Inaccessible form (unsemantic HTML, missing ARIA)
- XSS vulnerability (Html.Raw usage)
- Missing antiforgery token
- Hardcoded secrets
- Focus trap

**Action:** Auto-fix if possible. If not auto-fixable, ask user to override or request fixes.

### Step 2: Check Auto-Fixable Warnings
Apply auto-fixes:
- Missing color contrast → Adjust colors
- Missing ARIA attributes → Add labels
- Poor keyboard navigation → Fix tab order
- Missing touch target size → Increase button size
- Missing responsive styles → Add media queries
- Add async/await to database operations

### Step 3: Check Non-Auto-Fixable Warnings
Report to user:
- Missing XML documentation comments
- Could benefit from output caching
- No error handling for async operations

**Action:** Warn but allow proceeding.

### Step 4: Output Result

**If all blocking rules pass + warnings auto-fixed:**
```
✓ VALIDATION PASS

All standards met:
  ✓ WCAG 2.1 AA accessibility
  ✓ Security checks (antiforgery, input validation)
  ✓ Performance optimizations
  ✓ Responsive design
  
Auto-fixes applied: 3
  - Fixed color contrast on labels
  - Added aria-describedby to inputs
  - Updated media queries

Ready to proceed to Stage 8...
```

**If blocking rule fails (not auto-fixable):**
```
✗ VALIDATION FAIL

Critical issues:
  ✗ Form missing @Html.AntiForgeryToken()
  ✗ No keyboard navigation support

Auto-fixes NOT available for these issues.

Options:
  [Override & Proceed] [Request Manual Fixes] [Cancel]
```

---

## Override Behavior

If user overrides failed validation:
```
⚠️  Proceeding with known accessibility/security issues:
  - Color contrast: 3.8:1 (need 4.5:1)
  - Missing ARIA labels on 2 inputs

Code will be generated but flagged as non-compliant.
User assumes responsibility for fixing before production.
```

---

All validation rules ensure generated Razor Pages code is accessible, secure, and production-ready.
