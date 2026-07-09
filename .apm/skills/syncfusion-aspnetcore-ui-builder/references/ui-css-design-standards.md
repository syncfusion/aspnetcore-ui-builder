# UI/CSS Design Standards (MANDATORY)

**Every generated page MUST follow these standards for professional UI.**

---

## 1. Layout Structure
```html
<!-- Semantic HTML structure -->
<main class="page-container" role="main">
  <header class="page-header">
    <h1>Page Title</h1>
  </header>
  
  <section class="page-content">
    <!-- Page content here -->
  </section>
  
  <footer class="page-footer">
    <!-- Footer info -->
  </footer>
</main>
```

---

## 2. Form Styling (Login, Registration, etc.)

**HTML Structure:**
```html
<form method="post" class="form-container">
  <div class="form-group">
    <label for="email" class="form-label">Email Address</label>
    <ejs-textbox id="email" 
                  name="Email" 
                  type="email"
                  placeholder="Enter your email"
                  floatLabelType="Always"
                  cssClass="form-input"
                  aria-label="Email address"></ejs-textbox>
  </div>
  
  <div class="form-group">
    <label for="password" class="form-label">Password</label>
    <ejs-textbox id="password" 
                  name="Password" 
                  type="password"
                  placeholder="Enter password"
                  floatLabelType="Always"
                  cssClass="form-input"
                  aria-label="Password"></ejs-textbox>
  </div>
  
  <div class="form-group checkbox">
    <input type="checkbox" id="remember" name="RememberMe" />
    <label for="remember" class="form-label-inline">Remember me</label>
  </div>
  
  <button type="submit" class="btn btn-primary btn-block">Sign In</button>
</form>
```

**CSS Styling:**
```css
/* Form Container */
.form-container {
  max-width: 420px;
  margin: 2rem auto;
  padding: 2rem;
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

/* Form Groups */
.form-group {
  margin-bottom: 1.5rem;
  display: flex;
  flex-direction: column;
}

.form-group.checkbox {
  flex-direction: row;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

/* Labels */
.form-label {
  font-weight: 600;
  color: #333333;
  margin-bottom: 0.5rem;
  font-size: 0.95rem;
}

.form-label-inline {
  font-weight: 500;
  color: #555555;
  cursor: pointer;
}

/* Input Fields */
.form-input {
  border: 1px solid #d0d0d0;
  border-radius: 4px;
  padding: 0.75rem;
  font-size: 1rem;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.form-input:focus {
  border-color: #0066cc;
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
  outline: none;
}

/* Buttons */
.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
}

.btn-primary {
  background: linear-gradient(135deg, #0066cc 0%, #0052a3 100%);
  color: #ffffff;
}

.btn-primary:hover {
  background: linear-gradient(135deg, #0052a3 0%, #003d7a 100%);
  box-shadow: 0 4px 12px rgba(0, 102, 204, 0.3);
}

.btn-primary:active {
  transform: translateY(1px);
}

.btn-block {
  width: 100%;
}

/* Links */
.form-link {
  color: #0066cc;
  text-decoration: none;
  font-size: 0.9rem;
}

.form-link:hover {
  text-decoration: underline;
}

/* Responsive */
@media (max-width: 480px) {
  .form-container {
    margin: 1rem;
    padding: 1.5rem;
  }
  
  .form-label {
    font-size: 0.9rem;
  }
  
  .btn {
    padding: 0.6rem 1.2rem;
    font-size: 0.95rem;
  }
}
```

---

## 3. Color Scheme Standards

```css
/* Primary Colors */
--primary-color: #0066cc;
--primary-dark: #0052a3;
--primary-light: #e6f0ff;

/* Neutral Colors */
--text-primary: #333333;
--text-secondary: #666666;
--text-tertiary: #999999;
--background: #ffffff;
--border: #d0d0d0;

/* Semantic Colors */
--success: #28a745;
--error: #dc3545;
--warning: #ffc107;
--info: #17a2b8;

/* Accessibility - Text Contrast Ratios */
/* Primary text on white: 4.5:1+ (WCAG AA) */
/* Secondary text on white: 4.5:1+ (WCAG AA) */
/* Focus indicator: 3:1+ contrast */
```

---

## 4. Spacing & Layout Grid

```css
/* 8px spacing system */
--spacing-xs: 0.25rem;  /* 4px */
--spacing-sm: 0.5rem;   /* 8px */
--spacing-md: 1rem;     /* 16px */
--spacing-lg: 1.5rem;   /* 24px */
--spacing-xl: 2rem;     /* 32px */
--spacing-2xl: 3rem;    /* 48px */

/* Container widths */
--container-sm: 320px;
--container-md: 768px;
--container-lg: 1024px;
--container-xl: 1200px;
```

---

## 5. Typography Standards

```css
/* Font Stack */
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;

/* Heading Hierarchy */
h1 { font-size: 2rem; font-weight: 700; line-height: 1.2; }
h2 { font-size: 1.5rem; font-weight: 600; line-height: 1.3; }
h3 { font-size: 1.25rem; font-weight: 600; line-height: 1.4; }
h4 { font-size: 1.1rem; font-weight: 600; line-height: 1.4; }
h5 { font-size: 1rem; font-weight: 600; line-height: 1.5; }

/* Body Text */
body { font-size: 1rem; line-height: 1.6; color: #333333; }
small { font-size: 0.875rem; }

/* Letter Spacing */
h1, h2, h3 { letter-spacing: -0.5px; }
```

---

## 6. Syncfusion Component Styling

```css
/* Syncfusion inputs should match form styling */
.e-input-group {
  border-radius: 4px;
  border: 1px solid #d0d0d0;
}

.e-input-group:focus-within {
  border-color: #0066cc;
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
}

/* Syncfusion buttons */
.e-btn {
  border-radius: 4px;
  text-transform: none;
  font-weight: 600;
  padding: 0.75rem 1.5rem;
}

.e-btn.e-primary {
  background: #0066cc;
}

.e-btn.e-primary:hover {
  background: #0052a3;
}

/* Syncfusion Grid */
.e-grid {
  background: #ffffff;
  border-radius: 4px;
  overflow: hidden;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.e-gridheader {
  background: #f5f5f5;
  color: #333333;
  font-weight: 600;
}

.e-gridcontent .e-row:hover {
  background: #f9f9f9;
}

/* Syncfusion DropDownList */
.e-ddl {
  border-radius: 4px;
  border: 1px solid #d0d0d0;
}

.e-ddl:focus {
  border-color: #0066cc;
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
}
```

---

## CSS Generation Checklist

When generating CSS for ANY page, ensure:

- [ ] Start with CSS variables for colors/spacing (allows theming)
- [ ] Use mobile-first approach (base styles, then expand for larger screens)
- [ ] Include media queries at: 480px, 768px, 1024px
- [ ] Use flexbox/grid for layouts (NO fixed widths)
- [ ] Ensure 4.5:1 color contrast minimum (WCAG AA)
- [ ] All interactive elements ≥ 44x44px (touch target size)
- [ ] Use 8px spacing system throughout
- [ ] Style semantic HTML elements (h1, h2, form, button)
- [ ] Include Syncfusion component customization
- [ ] Add print styles if content is printable
- [ ] Transitions for interactive elements (0.3s typical)
- [ ] Focus states visible and accessible

---

## Complete Example: Professional Login Page

```html
@page
@model LoginPageModel

<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Login</title>
    <link rel="stylesheet" href="~/css/login.css">
</head>
<body>
    <main class="page-container" role="main">
        <div class="login-wrapper">
            <div class="login-card">
                <h1 class="login-title">Sign In</h1>
                
                <form method="post" class="form-container">
                    <div class="form-group">
                        <label for="email" class="form-label">Email Address</label>
                        <ejs-textbox id="email" 
                                      name="Email" 
                                      type="email"
                                      placeholder="Enter your email"
                                      floatLabelType="Always"
                                      cssClass="form-input"
                                      aria-label="Email address"></ejs-textbox>
                    </div>
                    
                    <div class="form-group">
                        <label for="password" class="form-label">Password</label>
                        <ejs-textbox id="password" 
                                      name="Password" 
                                      type="password"
                                      placeholder="Enter password"
                                      floatLabelType="Always"
                                      cssClass="form-input"
                                      aria-label="Password"></ejs-textbox>
                    </div>
                    
                    <div class="form-group checkbox">
                        <input type="checkbox" id="remember" name="RememberMe" />
                        <label for="remember" class="form-label-inline">Remember me</label>
                    </div>
                    
                    <button type="submit" class="btn btn-primary btn-block">Sign In</button>
                    
                    <p class="login-footer">
                        Don't have an account? 
                        <a href="/register" class="form-link">Register here</a>
                    </p>
                </form>
            </div>
        </div>
    </main>
</body>
</html>
```

**Associated CSS (login.css):**
```css
:root {
    --primary-color: #0066cc;
    --primary-dark: #0052a3;
    --text-primary: #333333;
    --border: #d0d0d0;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    min-height: 100vh;
}

.page-container {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 1rem;
}

.login-wrapper {
    width: 100%;
    max-width: 420px;
}

.login-card {
    background: white;
    border-radius: 8px;
    padding: 2rem;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
}

.login-title {
    font-size: 1.75rem;
    font-weight: 700;
    color: var(--text-primary);
    margin-bottom: 1.5rem;
    text-align: center;
}

.form-container {
    display: flex;
    flex-direction: column;
}

.form-group {
    margin-bottom: 1.5rem;
    display: flex;
    flex-direction: column;
}

.form-label {
    font-weight: 600;
    color: var(--text-primary);
    margin-bottom: 0.5rem;
    font-size: 0.95rem;
}

.form-input {
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 0.75rem;
    font-size: 1rem;
    transition: border-color 0.3s, box-shadow 0.3s;
}

.form-input:focus {
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
    outline: none;
}

.btn {
    padding: 0.75rem 1.5rem;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
}

.btn-primary {
    background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
    color: white;
    margin-top: 1rem;
}

.btn-primary:hover {
    box-shadow: 0 4px 12px rgba(0, 102, 204, 0.3);
    transform: translateY(-2px);
}

.btn-primary:active {
    transform: translateY(0);
}

.login-footer {
    text-align: center;
    margin-top: 1.5rem;
    font-size: 0.9rem;
    color: #666666;
}

.form-link {
    color: var(--primary-color);
    text-decoration: none;
}

.form-link:hover {
    text-decoration: underline;
}

/* Responsive */
@media (max-width: 480px) {
    .login-card {
        padding: 1.5rem;
    }
    
    .login-title {
        font-size: 1.5rem;
        margin-bottom: 1rem;
    }
    
    .form-group {
        margin-bottom: 1rem;
    }
}
```

---

## 7. Text Overflow & Truncation Standards

**Prevent text overflow glitches across all components:**

```css
/* Single-line text truncation with ellipsis */
.truncate-single {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

/* Multi-line text truncation (2-3 lines max) */
.truncate-lines {
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
    overflow: hidden;
    word-break: break-word;
}

/* Safe text wrapping - prevent overlap */
.text-wrap-safe {
    word-wrap: break-word;
    overflow-wrap: break-word;
    word-break: break-word;
    white-space: normal;
}

/* Log/code text handling - preserve formatting */
.log-text {
    font-family: 'Courier New', Courier, monospace;
    white-space: pre-wrap;
    word-break: break-all;
    overflow-wrap: break-word;
    max-width: 100%;
    padding: 0.5rem;
}

/* Table cells - prevent text overlap */
.table-cell {
    overflow: hidden;
    text-overflow: ellipsis;
    word-break: break-word;
    min-width: 0; /* Critical for flex/grid containers */
}

/* Form labels - prevent clipping */
.form-label {
    display: block;
    word-wrap: break-word;
    overflow-wrap: break-word;
    line-height: 1.4;
    margin-bottom: 0.5rem;
}

/* Tree/List item text - ensure visibility */
.tree-item-text,
.list-item-text {
    display: inline-block;
    vertical-align: middle;
    word-break: break-word;
    overflow-wrap: break-word;
    max-width: calc(100% - 2rem); /* Account for icons/spacing */
}
```

---

## 8. Tree & List Component Standards

**Fix tree nodes and list items displaying missing labels:**

```css
/* Tree component structure */
.e-treeview {
    background: var(--background, #ffffff);
}

.e-treeview .e-list-item {
    display: flex;
    align-items: center;
    padding: var(--spacing-md) var(--spacing-sm);
    min-height: 36px;
}

.e-treeview .e-list-item-text {
    display: block;
    flex: 1;
    margin-left: var(--spacing-md);
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    word-break: break-word;
}

.e-treeview .e-icons {
    flex-shrink: 0;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    min-width: 24px;
    min-height: 24px;
}

/* List component structure */
.e-listview {
    background: var(--background, #ffffff);
}

.e-listview .e-list-item {
    display: flex;
    align-items: center;
    padding: var(--spacing-md);
    min-height: 44px;
}

.e-listview .e-list-text {
    display: block;
    flex: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

/* Nested items - ensure proper spacing */
.e-treeview .e-list-item .e-list-item {
    margin-left: var(--spacing-lg);
    border-left: 2px solid var(--border, #e5e7eb);
    padding-left: var(--spacing-md);
}

/* Expanded/collapsed states */
.e-treeview .e-list-item.e-expanded > .e-icons::before {
    content: '▼';
}

.e-treeview .e-list-item:not(.e-expanded) > .e-icons::before {
    content: '▶';
}
```

---

## 9. Image Sizing & Aspect Ratio Standards

**Prevent image distortion and sizing issues:**

```css
/* Modal/Detail image sizing */
.modal-image,
.detail-image {
    max-width: 100%;
    height: auto;
    display: block;
    border-radius: var(--radius-md, 8px);
    object-fit: contain; /* Preserve aspect ratio */
}

/* Card image sizing */
.card-image {
    width: 100%;
    height: auto;
    max-height: 300px;
    object-fit: cover;
    border-radius: var(--radius-md, 8px) var(--radius-md, 8px) 0 0;
}

/* Thumbnail images */
.thumbnail-image {
    width: 100%;
    max-width: 200px;
    height: 200px;
    object-fit: cover;
    border-radius: var(--radius-md, 8px);
}

/* Product grid images */
.product-image {
    width: 100%;
    aspect-ratio: 1 / 1;
    object-fit: cover;
    border-radius: var(--radius-md, 8px);
    background: var(--skeleton-bg, #f0f0f0);
}

/* Avatar/profile images */
.avatar-image {
    width: 44px;
    height: 44px;
    border-radius: 50%;
    object-fit: cover;
    flex-shrink: 0;
}

/* Background images - prevent overflow */
.bg-image {
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    min-height: 200px;
}

/* Container for images - prevent layout shift */
.image-container {
    position: relative;
    width: 100%;
    padding-bottom: 66.66%; /* 3:2 aspect ratio */
    overflow: hidden;
    border-radius: var(--radius-md, 8px);
}

.image-container img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
}
```

---

## 10. Component Spacing & Alignment Standards

**Fix text overlap and alignment issues in complex components:**

```css
/* Appointment/Schedule items - prevent time/status overlap */
.appointment-item {
    display: flex;
    align-items: center;
    gap: var(--spacing-md, 16px);
    padding: var(--spacing-md);
    min-height: 44px;
    border-bottom: 1px solid var(--border, #e5e7eb);
}

.appointment-time {
    flex-shrink: 0;
    min-width: 80px;
    font-weight: 600;
    text-align: right;
    white-space: nowrap;
}

.appointment-label {
    flex: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    min-width: 0;
}

.appointment-status {
    flex-shrink: 0;
    padding: 0.25rem 0.75rem;
    border-radius: 4px;
    font-size: 0.85rem;
    font-weight: 600;
    white-space: nowrap;
}

/* Data grid rows - prevent text overflow */
.grid-row {
    display: flex;
    align-items: center;
    padding: var(--spacing-md);
    min-height: 44px;
    border-bottom: 1px solid var(--border, #e5e7eb);
}

.grid-cell {
    flex: 1;
    min-width: 0; /* Critical for text truncation in flex */
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    padding: var(--spacing-sm);
}

.grid-cell:first-child {
    padding-left: 0;
}

/* Card grid - ensure proper spacing */
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: var(--spacing-lg, 24px);
    padding: var(--spacing-lg);
}

.card {
    display: flex;
    flex-direction: column;
    height: 100%;
    padding: var(--spacing-lg);
    border-radius: var(--radius-lg, 12px);
    border: 1px solid var(--border, #e5e7eb);
    background: var(--background, #ffffff);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.card-content {
    flex: 1;
    min-height: 0; /* Allow proper overflow handling */
    overflow: hidden;
}

.card-title {
    font-weight: 600;
    font-size: 1rem;
    margin-bottom: var(--spacing-md);
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
}

.card-description {
    font-size: 0.9rem;
    color: var(--text-secondary, #666);
    line-height: 1.5;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
}

/* Modal/Dialog spacing */
.modal-content {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
    padding: var(--spacing-2xl, 32px);
    max-height: 90vh;
    overflow-y: auto;
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: var(--spacing-lg);
    margin-bottom: var(--spacing-lg);
}

.modal-body {
    flex: 1;
    overflow-y: auto;
    min-height: 0;
}

.modal-footer {
    display: flex;
    justify-content: flex-end;
    gap: var(--spacing-md);
    padding-top: var(--spacing-lg);
    border-top: 1px solid var(--border, #e5e7eb);
    flex-wrap: wrap;
}
```

---

## 11. Card Decoration Standards

**Proper handling of borders, underlines, and decorative elements:**

```css
/* Card borders - no unwanted decoration */
.card {
    border: 1px solid var(--border-color, #e5e7eb);
    border-bottom: 1px solid var(--border-color, #e5e7eb);
    /* Remove red/colored underlines unless intentional */
    text-decoration: none;
}

.card:hover {
    border-color: var(--border-hover, #d1d5db);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    text-decoration: none; /* Prevent hover underline */
}

/* List item borders */
.list-item {
    border-bottom: 1px solid var(--border-color, #e5e7eb);
    padding: var(--spacing-md);
}

.list-item:last-child {
    border-bottom: none;
}

/* Links in cards - control underlines */
.card-link {
    color: var(--primary-color, #0066cc);
    text-decoration: none;
    border-bottom: none;
    transition: color 0.2s;
}

.card-link:hover {
    color: var(--primary-dark, #0052a3);
    text-decoration: underline;
}

/* Remove unwanted borders on elements */
.unstyled {
    border: none;
    text-decoration: none;
    background: transparent;
}

/* Table/grid styling */
.table-header {
    background: var(--header-bg, #f5f5f5);
    border-bottom: 2px solid var(--border-color, #d0d0d0);
    font-weight: 600;
}

.table-row {
    border-bottom: 1px solid var(--border-color, #e5e7eb);
}

.table-row:hover {
    background: var(--hover-bg, #f9f9f9);
}
```

---

## 12. Responsive Overflow Handling

**Mobile-friendly text and spacing adjustments:**

```css
/* Mobile: prevent horizontal overflow */
@media (max-width: 640px) {
    .truncate-lines {
        -webkit-line-clamp: 2;
    }
    
    .grid-cell {
        font-size: 0.9rem;
        padding: var(--spacing-sm);
    }
    
    .appointment-time {
        min-width: 70px;
        font-size: 0.9rem;
    }
    
    .card-grid {
        grid-template-columns: 1fr;
        gap: var(--spacing-md);
    }
    
    .modal-content {
        padding: var(--spacing-lg);
        max-height: 95vh;
    }
    
    .table-cell {
        font-size: 0.85rem;
    }
}

/* Tablet: optimize spacing */
@media (min-width: 640px) and (max-width: 1024px) {
    .card-grid {
        grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    }
    
    .appointment-item {
        padding: var(--spacing-md) var(--spacing-lg);
    }
}

/* Desktop: full spacing and optimal layouts */
@media (min-width: 1024px) {
    .card-grid {
        grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    }
    
    .grid-cell {
        padding: var(--spacing-md);
    }
}
```

---

## Design Standards Summary

Use these standards for ALL pages:
- 8px spacing grid
- Professional color scheme with 4.5:1 contrast minimum
- Mobile-first responsive design
- Semantic HTML with accessibility
- Consistent Syncfusion component styling
- Smooth transitions and hover states
- Touch-friendly interactive elements (44x44px minimum)
- **Text truncation with ellipsis for overflow text**
- **Proper image sizing with aspect ratio preservation**
- **Component spacing to prevent text overlap**
- **Tree/list items with visible labels**
- **Responsive overflow handling for all screen sizes**
