# Layout Standards for All Page Types

**Generic layout patterns applicable to ALL page types (not component-specific).**

---

## Layout Architecture

**All pages follow this responsive container structure:**

```html
<div class="page-container">
    <!-- Optional: Header/AppBar -->
    <header class="page-header">
        <!-- Logo, title, navigation, user menu -->
    </header>
    
    <!-- Optional: Sidebar Navigation -->
    <nav class="page-sidebar">
        <!-- Navigation menu, links -->
    </nav>
    
    <!-- Main Content -->
    <main class="page-main">
        <section class="content-section">
            <!-- Page content -->
        </section>
    </main>
    
    <!-- Optional: Footer -->
    <footer class="page-footer">
        <!-- Footer content -->
    </footer>
</div>
```

---

## Page Layout Types

### 1. FULL-WIDTH PAGE (Forms, Single Content)
**Use for:** Registration forms, login, settings, single-purpose pages

```html
<div class="page-container">
    <main class="page-main" style="max-width: 800px; margin: 0 auto;">
        <section class="content-section">
            <h1>Form Title</h1>
            <!-- Form content here -->
        </section>
    </main>
</div>
```

**CSS Standard:**
```css
.page-main {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
}
```

---

### 2. SIDEBAR + CONTENT LAYOUT (Dashboards, Admin Panels)
**Use for:** Dashboards, admin panels, multi-section pages with navigation

```html
<div class="page-container" style="display: flex; min-height: 100vh;">
    <!-- Sidebar Navigation (optional: collapsible) -->
    <nav class="page-sidebar" style="width: 280px; flex-shrink: 0;">
        <!-- Navigation menu -->
    </nav>
    
    <!-- Main Content -->
    <main class="page-main" style="flex: 1; overflow-y: auto;">
        <header class="page-header">
            <!-- Header with toggle button -->
        </header>
        <section class="content-section">
            <!-- Page content -->
        </section>
    </main>
</div>
```

**CSS Standard:**
```css
.page-container {
    display: flex;
    min-height: 100vh;
}

.page-sidebar {
    width: 280px;
    background: var(--sidebar-bg, #ffffff);
    border-right: 1px solid var(--border-color, #e5e7eb);
    overflow-y: auto;
    flex-shrink: 0;
}

.page-main {
    flex: 1;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
}
```

**Sidebar Toggle (Responsive):**
```html
<button id="sidebarToggle" class="btn-toggle-sidebar">☰</button>

<script>
document.getElementById('sidebarToggle').addEventListener('click', function() {
    const sidebar = document.querySelector('.page-sidebar');
    sidebar.classList.toggle('collapsed');
});
</script>

<style>
@media (max-width: 768px) {
    .page-sidebar {
        position: absolute;
        left: 0;
        top: 0;
        height: 100%;
        z-index: 1000;
        transform: translateX(-100%);
        transition: transform 0.3s ease;
    }
    
    .page-sidebar.expanded {
        transform: translateX(0);
    }
}
</style>
```

---

### 3. HEADER + CONTENT LAYOUT (Simple Pages)
**Use for:** Product listings, simple content pages, galleries

```html
<div class="page-container">
    <header class="page-header">
        <!-- Navigation and branding -->
    </header>
    <main class="page-main">
        <section class="content-section">
            <!-- Page content -->
        </section>
    </main>
</div>
```

---

### 4. THREE-COLUMN LAYOUT (Complex Dashboards)
**Use for:** Analytics dashboards, detail + context pages

```html
<div class="page-container" style="display: flex; min-height: 100vh;">
    <nav class="page-sidebar" style="width: 250px;">
        <!-- Navigation -->
    </nav>
    
    <main class="page-main" style="flex: 1;">
        <header class="page-header">
            <!-- Header -->
        </header>
        
        <div style="display: grid; grid-template-columns: 200px 1fr; gap: 2rem; padding: 2rem;">
            <aside class="sidebar-secondary">
                <!-- Filters, secondary nav -->
            </aside>
            <section class="content-primary">
                <!-- Main content -->
            </section>
        </div>
    </main>
</div>
```

---

## Spacing & Grid Standards

**All layouts use 8px base grid system:**

```css
:root {
    --spacing-xs: 0.25rem;   /* 4px */
    --spacing-sm: 0.5rem;    /* 8px - BASE */
    --spacing-md: 1rem;      /* 16px */
    --spacing-lg: 1.5rem;    /* 24px */
    --spacing-xl: 2rem;      /* 32px */
    --spacing-2xl: 3rem;     /* 48px */
    
    --radius-sm: 0.375rem;   /* 6px */
    --radius-md: 0.5rem;     /* 8px */
    --radius-lg: 0.75rem;    /* 12px */
}

/* Consistent spacing in all sections */
.content-section {
    padding: var(--spacing-xl) var(--spacing-2xl);
    margin-bottom: var(--spacing-2xl);
}

.section-title {
    font-size: 1.375rem;
    font-weight: 600;
    margin-bottom: var(--spacing-lg);
    padding-bottom: var(--spacing-md);
    border-bottom: 2px solid var(--primary-500);
}
```

---

## Responsive Breakpoints

**Mobile-first approach with these breakpoints:**

```css
/* Mobile (base): 320px+ */
.page-main {
    padding: var(--spacing-md);
}

/* Tablet: 640px+ */
@media (min-width: 640px) {
    .page-main {
        padding: var(--spacing-lg);
    }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
    .page-main {
        padding: var(--spacing-xl);
    }
}

/* Wide: 1280px+ */
@media (min-width: 1280px) {
    .page-main {
        max-width: 1400px;
    }
}
```

---

## Header Component Pattern

**Standard header structure for all pages:**

```html
<header class="page-header">
    <div class="header-left">
        <!-- Toggle button (if sidebar) + Logo/Title -->
        <button id="sidebarToggle" class="btn-toggle-sidebar">☰</button>
        <h1 class="page-title">Page Title</h1>
    </div>
    
    <div class="header-right">
        <!-- Actions, search, user menu -->
        <div class="user-menu">
            <span class="user-name">John Doe</span>
            <img src="..." alt="User" class="user-avatar">
        </div>
    </div>
</header>

<style>
.page-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: var(--spacing-md) var(--spacing-xl);
    background: var(--header-bg, #ffffff);
    border-bottom: 1px solid var(--border-color, #e5e7eb);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    min-height: 70px;
}

.header-left {
    display: flex;
    align-items: center;
    gap: var(--spacing-lg);
}

.page-title {
    font-size: 1.75rem;
    font-weight: 600;
    margin: 0;
}
</style>
```

---

## Sidebar Navigation Pattern

**Standard sidebar structure (can be collapsed):**

```html
<nav class="page-sidebar">
    <!-- Brand Section -->
    <div class="sidebar-brand">
        <h3>Dashboard</h3>
    </div>
    
    <!-- Navigation Items -->
    <ul class="sidebar-menu">
        <li class="menu-item active">
            <a href="#" class="menu-link">
                <span class="menu-icon">📊</span>
                <span class="menu-text">Dashboard</span>
            </a>
        </li>
        <li class="menu-item">
            <a href="#" class="menu-link">
                <span class="menu-icon">📈</span>
                <span class="menu-text">Analytics</span>
            </a>
        </li>
        <li class="menu-divider"></li>
        <li class="menu-item">
            <a href="#" class="menu-link">
                <span class="menu-icon">⚙️</span>
                <span class="menu-text">Settings</span>
            </a>
        </li>
    </ul>
</nav>

<style>
.sidebar-brand {
    padding: var(--spacing-lg) var(--spacing-md);
    border-bottom: 1px solid var(--border-color);
}

.sidebar-menu {
    list-style: none;
    padding: var(--spacing-md) 0;
}

.menu-item {
    margin: var(--spacing-xs) 0;
}

.menu-link {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
    padding: var(--spacing-md) var(--spacing-lg);
    text-decoration: none;
    color: var(--text-secondary);
    transition: all 0.2s ease;
    border-left: 3px solid transparent;
}

.menu-link:hover {
    background: var(--hover-bg);
    color: var(--primary-600);
    border-left-color: var(--primary-500);
}

.menu-item.active .menu-link {
    background: var(--primary-100);
    color: var(--primary-600);
    border-left-color: var(--primary-500);
    font-weight: 500;
}
</style>
```

---

## Content Grids

**Standard grid patterns for all content types:**

```css
/* KPI Cards - Auto-fit responsive grid */
.kpi-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: var(--spacing-lg);
}

/* Charts - Responsive 2-column on desktop, 1 on mobile */
.charts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: var(--spacing-lg);
}

/* Product Grid - Flexible columns */
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: var(--spacing-lg);
}

/* Mobile: all grids collapse to single column */
@media (max-width: 768px) {
    .kpi-grid,
    .charts-grid,
    .product-grid {
        grid-template-columns: 1fr;
    }
}
```

---

## Card Component Standard

**Used for KPI cards, product cards, data cards:**

```html
<div class="card">
    <div class="card-header">
        <h3 class="card-title">Title</h3>
        <span class="card-icon">📊</span>
    </div>
    <p class="card-value">$125,450</p>
    <p class="card-meta">+12.5% vs last month</p>
</div>

<style>
.card {
    background: var(--card-bg, #ffffff);
    border-radius: var(--radius-lg);
    padding: var(--spacing-lg);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    border: 1px solid var(--border-color, #e5e7eb);
    transition: all 0.3s ease;
}

.card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--spacing-md);
}

.card-title {
    font-size: 0.95rem;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin: 0;
}

.card-value {
    font-size: 2rem;
    font-weight: 700;
    margin: 0 0 var(--spacing-sm) 0;
}

.card-meta {
    font-size: 0.85rem;
    color: var(--text-secondary);
    margin: 0;
}
</style>
```

---

## Syncfusion Component Integration

**Standard styling for Syncfusion grids, charts, dropdowns:**

```css
/* Syncfusion Grid */
.e-grid {
    background: var(--card-bg);
    border-radius: var(--radius-lg);
    overflow: hidden;
    box-shadow: var(--card-shadow);
}

.e-gridheader {
    background: var(--gray-100);
    color: var(--gray-900);
    font-weight: 600;
}

.e-gridcontent .e-row:hover {
    background: var(--gray-50);
}

/* Syncfusion Input */
.e-textbox, .e-ddl {
    border-radius: var(--radius-md);
    border: 1px solid var(--border-color);
}

.e-textbox:focus, .e-ddl:focus {
    border-color: var(--primary-500);
    box-shadow: 0 0 0 3px var(--primary-100);
}

/* Syncfusion Button */
.e-btn {
    border-radius: var(--radius-md);
    text-transform: none;
    font-weight: 500;
}

.e-btn.e-primary {
    background: var(--primary-500);
}

.e-btn.e-primary:hover {
    background: var(--primary-600);
}
```

---

## Implementation Checklist

When generating any page, ensure:

- [ ] Layout type selected (full-width / sidebar / header+content / three-column)
- [ ] Container structure matches pattern above
- [ ] 8px grid spacing applied throughout
- [ ] Responsive breakpoints implemented (320px, 640px, 1024px, 1280px)
- [ ] CSS variables used for colors, spacing, radius
- [ ] Header component included (if needed)
- [ ] Sidebar structure correct (if needed)
- [ ] Card components used for content grouping
- [ ] Syncfusion components styled consistently
- [ ] Mobile-first approach (base styles work on mobile)
- [ ] All grids responsive (auto-fit or auto-fill)

---

## Layout Selection Guide

| Page Type | Best Layout | Use When |
|-----------|------------|----------|
| Login | Full-width | Single-purpose authentication |
| Registration | Full-width | Sign-up form |
| Settings | Full-width | User preferences, simple forms |
| Dashboard | Sidebar + Content | Multiple navigation sections |
| Admin Panel | Sidebar + Content | Complex application with menu |
| Product List | Header + Content | Simple product catalog |
| Blog | Header + Content | Content-focused pages |
| Analytics | Three-column | Dashboard with filters and data |
| Reports | Three-column | Complex data visualization |

---

## Quick CSS Template

**Copy and customize for any page:**

```css
:root {
    --primary-500: #3b82f6;
    --primary-600: #2563eb;
    --gray-100: #f3f4f6;
    --gray-900: #111827;
    --border-color: #e5e7eb;
    --spacing-md: 1rem;
    --spacing-lg: 1.5rem;
    --spacing-xl: 2rem;
}

.page-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: var(--spacing-xl);
}

.page-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--spacing-2xl);
    padding-bottom: var(--spacing-lg);
    border-bottom: 1px solid var(--border-color);
}

.page-main {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
}

.content-section {
    background: white;
    border-radius: 8px;
    padding: var(--spacing-lg);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

/* Responsive */
@media (max-width: 1024px) {
    .page-container {
        padding: var(--spacing-lg);
    }
}

@media (max-width: 640px) {
    .page-container {
        padding: var(--spacing-md);
    }
    
    .page-header {
        flex-direction: column;
        gap: var(--spacing-md);
    }
}
```
