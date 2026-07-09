# Syncfusion ASP.NET Core UI Builder

**Syncfusion ASP.NET Core UI Builder** is an AI-powered agent skill that transforms your UI requirements into production-ready ASP.NET Core components. It leverages Syncfusion's extensive ASP.NET Core UI component library to generate accessible, responsive, and theme-consistent user interfaces.

### Key Features

- **AI Agent Orchestration**: Intelligent workflow handling design thinking, component selection, code generation, and validation
- **Syncfusion Integration**: Access to professional ASP.NET Core UI components
- **WCAG 2.1 AA Accessibility**: Built-in accessibility compliance with semantic HTML and ARIA support
- **Responsive Design**: Mobile-first CSS with adaptive breakpoints
- **Design System Support**: Bootstrap 5, Tailwind CSS, or Material 3 theming with Syncfusion theme alignment
- **Razor Components**: Full type coverage for models, ViewComponents, and Tag Helpers

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [How It Works](#how-it-works)
- [Usage](#usage)
- [Support](#Support)

## Prerequisites

Before using ASP.NET Core UI Builder, ensure your environment meets these requirements:

| Requirement | Description |
|-------------|-------------|
| **Microsoft .NET SDK 8.0 or later** | .NET CLI tools installed |
| **Node.js version 18 or later** | npm package manager installed |
| **Agent Package Manager (APM)** | Agent Package Manager installed. [Installation Guidelines](https://microsoft.github.io/apm/quickstart/#1-install-apm) |
| **ASP.NET Core Project** | Active ASP.NET Core MVC, Razor Pages |
| **Syncfusion License** | [Commercial](https://www.syncfusion.com/sales/unlimitedlicense), [Free Community](https://www.syncfusion.com/products/communitylicense), or [Free Trial](https://www.syncfusion.com/account/manage-trials/start-trials) |

## Installation

```bash
# Install for GitHub Copilot
apm install syncfusion/aspnetcore-ui-builder -t copilot

# Install for Claude Code
apm install syncfusion/aspnetcore-ui-builder -t claude

# Install for Cursor
apm install syncfusion/aspnetcore-ui-builder -t cursor

# Install for Codex
apm install syncfusion/aspnetcore-ui-builder -t codex

```

## How It Works

The ASP.NET Core UI Builder uses an **8-stage AI orchestration workflow** that transforms your requirements into production-ready components.

**Stage 1: Intent Analysis**
Parse the user's natural language query to identify component types, layout intent, and desired functionality.

**Stage 2: Project Detection**
Automatically detect the project framework (MVC, Razor Pages), .NET version, and existing theme configuration.

**Stage 3: Component Mapping**
Select appropriate Syncfusion components and their required icons based on the identified intent.

**Stage 4: Theming & Design System**
Lock in design system decisions including CSS framework, Syncfusion theme (Bootstrap5, Tailwind, Material3), color modes (light, dark) colors, spacing, typography upon users confirmation.

**Stage 5: Code Generation**
Produce Razor view components, Tag Helpers components with full model binding and CSS/styling scaffolding.

**Stage 6: Dependency Management**
Install required Syncfusion NuGet packages and their dependencies.

**Stage 7: Validation**
Run WCAG accessibility checks, security scans, and performance audits. Request approval before code insertion.

**Stage 8: Code Insertion**
Create new files or patch existing ones following the project's structure and coding conventions.

## Usage

Choose the `syncfusion-aspnetcore-ui-builder` agent in the AI chat panel and invoke the skill through your AI assistant by describing what you want to build:

```
Create a CMS Admin Dashboard UI featuring a collapsible sidebar with navigation items for Dashboard, Content, Users, Analytics, and Settings; a top header (AppBar) showing the title “CMS Admin Dashboard” on the left and a user name with profile icon on the right; and a main content area that includes three compact summary cards in a single row displaying Total Content, Total Users, and Active Sessions (each card showing a label, relevant icon, prominent count value, and percentage change from last month), followed by a “Content Management” section with a filterable and data grid containing columns for Title, Author, Status, Date, and Actions (with edit and delete buttons), and finally two charts displayed side by side—a bar chart titled “Content Over Time” and a donut chart titled “Content by Category”—using realistic sample data for both the grid (10–12 rows) and the charts.
```

Generated code follows best practices with accessible, semantic HTML, responsive mobile-first layouts, strong model binding, and built-in security measures such as input validation and avoidance of hardcoded secrets.

## Best Practices
- Maintain consistency in file structure, naming, and coding standards.
- Use advanced AI models (e.g., Claude Sonnet 4.6+) for better code quality.
- Review everything before production—replace placeholders and verify logic, security, and compatibility.

## License

Syncfusion® ASP.NET Core Components is available under the Syncfusion® Essential Studio program, and can be licensed either under the Syncfusion® Community License Program or the Syncfusion commercial license.

To be qualified for the Syncfusion® Community License Program, you must have gross revenue of less than one (1) million U.S. dollars (USD 1,000,000.00) per year and have less than five (5) developers in your organization, and agree to be bound by Syncfusion's terms and conditions.

Customers who do not qualify for the community license can contact sales@syncfusion.com for commercial licensing options.

You may not use this product without first purchasing a Community License or a Commercial License, as well as agreeing to and complying with Syncfusion's license terms and conditions.

The Syncfusion® license that contains the terms and conditions can be found at
[https://www.syncfusion.com/content/downloads/syncfusion_license.pdf](https://www.syncfusion.com/content/downloads/syncfusion_license.pdf)

## Support & Feedback

Product support is available through the following media.

- [Support ticket](https://support.syncfusion.com/support/tickets/create) - Guaranteed response in 24 hours | Unlimited tickets | Holiday support
- [Community forum](https://www.syncfusion.com/forums/aspnetcore-js2)
- [Request feature or report bug](https://www.syncfusion.com/feedback/aspnet-core)
- [Live chat](https://www.syncfusion.com/support)

## See also

* [Syncfusion ASP.NET Core User-Guide](https://ej2.syncfusion.com/aspnetcore/documentation/introduction)
* [Syncfusion ASP.NET Core Components](https://www.syncfusion.com/aspnet-core-ui-controls)
* [Syncfusion ASP.NET Core Live Demos](https://ej2.syncfusion.com/aspnetcore/)

<p>Copyright © 2001-2026 Syncfusion®, Inc. All rights reserved.</p> 