# Shakti Insights & Analytics Portal

A production-grade analytics portal for centralizing and managing Power BI reports across multiple departments. Built with pure HTML, CSS, and JavaScript - no external dependencies required.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Configuration Guide](#configuration-guide)
- [Adding Content](#adding-content)
- [Customization](#customization)
- [Browser Support](#browser-support)
- [Deployment](#deployment)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [Troubleshooting](#troubleshooting)

## Overview

Shakti Insights Portal is a unified dashboard hub that organizes Power BI reports by department. It provides a clean, professional interface for non-technical users to access business intelligence dashboards without navigating complex Power BI workspaces.

**Key Capabilities:**
- Department-based report organization
- Category filtering within departments
- Fullscreen dashboard viewing
- Direct linking to Power BI reports
- Responsive design for desktop and tablet

## Features

### Core Features
- **Department Homepage** - Card-based department overview with report counts
- **Report Gallery** - Filterable grid view of all reports within a department
- **Dashboard Viewer** - Embedded Power BI iframe with fullscreen support
- **Context Menu** - Right-click/More menu for copy link and fullscreen
- **Breadcrumb Navigation** - Clear hierarchy showing current location
- **Collapsible Sidebar** - Space-saving navigation with department/report tree

### User Experience
- Smooth animations and transitions
- Loading states with spinner animation
- Visual feedback on all interactive elements
- Keyboard shortcuts for power users
- Mobile-friendly responsive layout

### Professional Features
- Category color-coding system
- Audit-ready status indicators
- Toast notifications for user actions
- Persistent navigation state
- Zero external dependencies (except Google Fonts)

## Architecture

```
Shakti Insights Portal
├── Data Layer (DEPTS array)
│   ├── Departments
│   └── Dashboards (Power BI URLs)
├── View Layer
│   ├── Home View (Department cards)
│   ├── Gallery View (Filterable reports)
│   └── Dashboard View (iframe embed)
├── Navigation Layer
│   ├── Sidebar Navigation
│   ├── Breadcrumb Trail
│   └── Top Bar Controls
└── Utility Layer
    ├── Fullscreen API
    ├── Clipboard API
    ├── Toast Notifications
    └── Responsive Handler
```

## Configuration Guide

### 1. Department Structure

Each department follows this schema:

```javascript
{
  id: "unique_identifier",        // Used for routing and keys
  name: "Display Name",            // Shown in UI
  icon: "🏛️",                     // Emoji or text icon
  desc: "Brief description",       // Shown on department card
  color: "linear-gradient(...)",   // Banner gradient
  dashboards: []                   // Array of report objects
}
```

### 2. Dashboard Structure

Each dashboard/report follows this schema:

```javascript
{
  id: "unique_identifier",         // Used for navigation
  label: "Short Name",             // Appears in sidebar
  title: "Full Report Title",      // Main heading
  category: "Category Name",       // Used for filtering and coloring
  subtitle: "Description",         // Additional context
  link: "POWER_BI_EMBED_URL"       // Full iframe src URL
}
```

### 3. Category Color System

Categories are automatically color-coded. Default mapping:

| Category | Primary Color |
|----------|---------------|
| Operations | Orange (#ea580c) |
| Recovery | Green (#16a34a) |
| Finance | Blue (#2563eb) |
| Health | Red (#dc2626) |
| HR | Yellow (#ca8a04) |
| IT | Purple (#7c3aed) |

## Adding Content

### Adding a New Department

Locate the `DEPTS` array in the JavaScript section and add:

```javascript
{
  id: "hr",
  name: "Human Resources",
  icon: "👥",
  desc: "Workforce analytics and talent management",
  color: "linear-gradient(135deg,#1c0a00,#431407,#7c2d12)",
  dashboards: [
    // Add dashboard objects here
  ]
}
```

### Adding a Dashboard to Existing Department

Find the department's `dashboards` array and add:

```javascript
{
  id: "attrition",
  label: "Attrition Analysis",
  title: "Monthly Attrition & Retention Report",
  category: "HR Analytics",
  subtitle: "Track attrition rates, retention metrics, and exit trends",
  link: "https://app.powerbi.com/view?r=YOUR_EMBED_CODE"
}
```

### Getting Power BI Embed URL

1. Open your Power BI report in the Power BI service
2. Click **File** → **Embed report** → **Publish to web (public)**
3. Copy the embed URL (format: `https://app.powerbi.com/view?r=...`)
4. **Important:** Use only for internal/public approved content

## Customization

### Changing Portal Name

The portal name appears in three locations:

1. **Sidebar Brand** (line ~190):
   ```html
   <div class="sb-portal-name">Shakti Insights</div>
   <div class="sb-portal-sub">Analytics Portal</div>
   ```

2. **Hero Section** (line ~340):
   ```html
   <div class="hero-name">
     Shakti Insights<br>
     <span class="hero-name-accent">&amp; Analytics Portal</span>
   </div>
   ```

3. **Breadcrumb Home** (line ~220):
   ```html
   <span class="bc-home" onclick="goHome()">Shakti Insights</span>
   ```

### Changing Color Scheme

Modify CSS variables in `:root` section:

```css
:root {
  --teal: #0d9488;        /* Primary brand color */
  --teal-mid: #0f766e;    /* Darker variant */
  --teal-pale: #f0fdfa;   /* Light background variant */
  --ink: #1c1917;         /* Text color */
  --sand: #faf9f7;        /* Page background */
}
```

### Department Banner Colors

Each department has its own gradient. Modify the `color` property:

```javascript
color: "linear-gradient(135deg, #START_COLOR 0%, #MID_COLOR 55%, #END_COLOR 100%)"
```

### Adding Custom Categories

Extend the `CAT` and `CAT_LINE` objects:

```javascript
const CAT = {
  "Your Category": ["#bgColor","#iconColor","#badgeBg","#badgeText"],
  // ...
};

const CAT_LINE = {
  "Your Category": "#borderColor",
  // ...
};
```

## Browser Support

| Browser | Minimum Version | Fullscreen Support |
|---------|----------------|-------------------|
| Chrome | 90+ | ✅ |
| Firefox | 88+ | ✅ |
| Edge | 90+ | ✅ |
| Safari | 14+ | ✅ |
| Opera | 75+ | ✅ |

**Note:** Requires JavaScript enabled. Fullscreen API requires user interaction.

## Deployment

### Option 1: Static Hosting (Recommended)

1. Save the HTML file as `index.html`
2. Upload to any static hosting service:
   - GitHub Pages
   - Netlify
   - Vercel
   - AWS S3 + CloudFront
   - Any web server

### Option 2: SharePoint/Intranet

1. Copy the HTML content
2. Add to a SharePoint Page web part (Embed/HTML)
3. Or save as `.html` and upload to document library

### Option 3: Local Network Server

```bash
# Using Python 3
python -m http.server 8080

# Using Node.js (http-server)
npx http-server -p 8080

# Using PHP
php -S localhost:8080
```

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Esc` | Go back one level (Dashboard → Gallery → Home) |
| `Ctrl/Cmd + B` | Toggle sidebar collapse |

## Troubleshooting

### Power BI Reports Not Loading

**Issue:** iframe stays blank with loader

**Solutions:**
1. Verify the Power BI embed URL is correct
2. Check if the report is published to web (public access)
3. Ensure no ad-blocker is blocking iframes
4. Check browser console for CSP (Content Security Policy) errors

**Note:** If using SharePoint or strict intranet policies, you may need to configure iframe allowances.

### Sidebar Not Collapsing

**Issue:** Sidebar remains open on mobile

**Solution:** The responsive design activates below 860px width. Check your viewport meta tag is present and device width is detected correctly.

### Category Colors Not Showing

**Issue:** Badges appear with default colors

**Solution:** Ensure category names exactly match keys in `CAT` object (case-sensitive). Use "Default" as fallback for uncategorized items.

### Fullscreen Not Working

**Issue:** Fullscreen button has no effect

**Solution:** 
- Fullscreen API requires user interaction (works after clicking dashboard)
- Check browser permissions for fullscreen
- Some browsers restrict fullscreen in iframes

## Security Considerations

⚠️ **Important:** When embedding Power BI reports:

1. **Public Embed:** The "Publish to web" option makes data publicly accessible
2. **Internal Use Only:** Use Power BI Embedded (requires license) for secure internal access
3. **No Authentication:** This portal does not handle user authentication
4. **Network Security:** Deploy behind appropriate network controls if hosting sensitive data

For secure embedding with authentication, consider:
- Power BI Embedded with Azure AD
- SharePoint Online with Power BI web part
- Power BI Report Server (on-premises)

## File Structure

```
shakti-portal/
├── index.html          # Complete application (single file)
├── README.md           # Documentation
└── assets/             # (Optional - any images/favicons)
    └── favicon.ico
```

## Performance Optimizations

- Lazy-loading iframes (only load when opened)
- CSS animations use GPU acceleration
- No external libraries - minimal payload (~50KB gzipped)
- Semantic HTML for fast rendering
- Efficient DOM updates with targeted operations

## Support & Maintenance

**Daily Tasks:**
- Update Power BI URLs when reports change
- Add new dashboards to appropriate departments
- Verify all links are functional

**Monthly Review:**
- Check for broken iframe links
- Review category color consistency
- Test on target browsers

**Quarterly Updates:**
- Audit department structure relevance
- Remove deprecated reports
- Review security for public embeds

---

**Version:** 1.0.0  
**Last Updated:** January 2026  
**Compatible with:** Power BI Service (Publish to Web)
