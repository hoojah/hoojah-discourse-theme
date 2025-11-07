# Development Guide

Guide for developing and customizing the Hoojah Discourse theme.

## Getting Started

### Prerequisites

- Access to a Discourse 3.1+ instance (local or staging)
- Basic knowledge of:
  - HTML/CSS
  - JavaScript (ES6+)
  - SCSS
  - Git

### Setup

1. **Fork the repository**
   ```bash
   git clone https://github.com/hoojah/hoojah-discourse-theme.git
   cd hoojah-discourse-theme
   ```

2. **Install on Discourse**
   - Admin → Customize → Themes
   - Install → From a git repository
   - Enter your repository URL

3. **Enable development mode**
   - Add `?safe_mode=no_themes` to test without theme
   - Use browser DevTools for debugging
   - Check Discourse logs for errors

## Theme Architecture

### File Structure

```
hoojah-discourse-theme/
├── common/               # Shared across desktop & mobile
│   ├── common.scss      # Base styles
│   └── head_tag.html    # JavaScript & meta tags
├── desktop/             # Desktop only (768px+)
│   └── desktop.scss
├── mobile/              # Mobile only (<768px)
│   └── mobile.scss
├── locales/             # Translations
│   └── en.yml
├── assets/              # Static assets
│   └── images/
└── Configuration files
    ├── about.json       # Theme metadata
    ├── settings.yml     # User-configurable settings
    └── .discourse-compatibility
```

### CSS/SCSS Guidelines

#### Using CSS Variables

Define variables in `common/common.scss`:

```scss
:root {
  --hoojah-primary: #415DE6;
  --hoojah-spacing: 1rem;
}

.my-component {
  color: var(--hoojah-primary);
  padding: var(--hoojah-spacing);
}
```

#### Responsive Design

Use media queries in appropriate files:

```scss
// mobile/mobile.scss
@media (max-width: 767px) {
  .my-component {
    padding: 0.5rem;
  }
}

// desktop/desktop.scss
@media (min-width: 768px) {
  .my-component {
    padding: 2rem;
  }
}
```

#### Discourse Variables

Use built-in Discourse SCSS variables:

```scss
.my-component {
  background: $primary-low;
  color: $primary;
  border: 1px solid $primary-medium;
}
```

Common variables:
- `$primary`, `$secondary`, `$tertiary`
- `$danger`, `$success`, `$love`
- `$primary-low`, `$primary-medium`, `$primary-high`

## JavaScript Development

### Modern Plugin API

Always use `withPluginApi` with version 1.14+:

```javascript
// common/head_tag.html
<script type="text/discourse-plugin" version="1.14">
const { withPluginApi } = require("discourse/lib/plugin-api");

withPluginApi("1.14", (api) => {
  const pluginId = "hoojah-theme";

  // Your code here
});
</script>
```

### Using Transformers (Modern Approach)

Transformers are the modern way to modify values:

```javascript
api.registerValueTransformer("category-name-formatter", ({ value, context }) => {
  // Modify category name display
  return value.toUpperCase();
});
```

### Plugin Outlets

Inject content at specific points:

```javascript
api.renderInOutlet("above-main-container", <template>
  <div class="custom-banner">
    <p>Welcome to Hoojah!</p>
  </div>
</template>);
```

Find available outlets using the [Plugin Outlet Locations](https://meta.discourse.org/t/plugin-outlet-locations-theme-component/100673) component.

### Accessing Theme Settings

```javascript
// In JavaScript
if (settings.enable_wide_layout) {
  document.body.classList.add("wide-layout");
}

// Get custom color
const brandColor = settings.brand_color;
```

```scss
// In SCSS
.my-component {
  @if $enable_wide_layout {
    max-width: 1400px;
  }
}
```

### Event Listeners

```javascript
api.onPageChange((url) => {
  console.log("Page changed to:", url);
  // Your logic here
});
```

### Decorating Components

For simple additions to existing components:

```javascript
api.decorateWidget("post:after", (helper) => {
  return helper.h("div.custom-footer", "Custom content");
});
```

## Common Customizations

### Custom Logo

1. Add upload setting in `settings.yml`:
   ```yaml
   brand_logo:
     type: upload
     default: ""
   ```

2. Use in template or CSS:
   ```scss
   .logo-big {
     content: url($brand_logo);
   }
   ```

### Custom Header Banner

```javascript
api.renderInOutlet("above-site-header", <template>
  <div class="hoojah-banner">
    <h2>Welcome to Hoojah:Bincang</h2>
  </div>
</template>);
```

### Modify Topic List

Use transformers instead of modifyClass:

```javascript
api.registerValueTransformer("topic-list-columns", ({ value }) => {
  // Add custom column
  value.push({
    name: "custom-column",
    labelKey: "custom.column.label"
  });
  return value;
});
```

### Custom User Menu Items

```javascript
api.addUserMenuGlyph((widget) => {
  return {
    label: "custom.menu.item",
    icon: "star",
    href: "/custom-page"
  };
});
```

## Debugging

### Browser Console

Check for errors:
```javascript
// Add debug logging
console.log("[Hoojah Theme]", "Debug info here");
```

### Discourse Logs

Check server logs for theme errors:
```bash
# In Discourse container
tail -f /var/www/discourse/log/production.log
```

### Safe Mode

Test without your theme:
```
https://your-forum.com/?safe_mode=no_themes
```

### Theme Errors

View theme errors in Admin:
- Admin → Customize → Themes
- Click on theme → View errors

## Testing

### Manual Testing Checklist

- [ ] Desktop view (1920x1080)
- [ ] Tablet view (768x1024)
- [ ] Mobile view (375x667)
- [ ] Dark mode (if supported)
- [ ] Different user states (logged in, logged out, admin)
- [ ] All major pages (home, topic, profile, categories)
- [ ] Theme settings work correctly

### Browser Testing

Test on:
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile Safari (iOS)
- Mobile Chrome (Android)

## Best Practices

### Performance

1. **Minimize JavaScript**: Keep JS lightweight
2. **Optimize CSS**: Remove unused styles
3. **Use CSS variables**: Better than duplicating values
4. **Lazy load**: Don't run code on every page if not needed

```javascript
// Good: Only run on specific pages
if (window.location.pathname.startsWith("/t/")) {
  // Topic-specific code
}
```

### Maintainability

1. **Comment your code**: Explain why, not what
2. **Use consistent naming**: Follow Discourse conventions
3. **Organize by feature**: Group related code together
4. **Version control**: Commit logical chunks

### Compatibility

1. **Check API version**: Use appropriate API methods
2. **Test on target Discourse version**: Don't use features from newer versions
3. **Graceful degradation**: Handle missing features
4. **Use transformers over modifyClass**: More stable

## Common Issues

### Theme Not Loading

1. Check browser console for errors
2. Verify `about.json` is valid JSON
3. Check minimum Discourse version
4. Review Admin → Logs for theme errors

### Styles Not Applying

1. Clear browser cache
2. Check CSS specificity
3. Ensure SCSS compiles without errors
4. Check file is in correct directory (common/desktop/mobile)

### JavaScript Not Working

1. Check Plugin API version matches
2. Verify `withPluginApi` is used correctly
3. Check for console errors
4. Ensure pluginId is set

### Settings Not Showing

1. Verify `settings.yml` syntax
2. Check setting type is valid
3. Restart Discourse if needed
4. Check locales file for translations

## Resources

### Official Documentation

- [Discourse Developer Docs](https://meta.discourse.org/c/dev/)
- [Theme Development Guide](https://meta.discourse.org/t/developer-s-guide-to-discourse-themes/93648)
- [Plugin API Documentation](https://github.com/discourse/discourse/blob/main/app/assets/javascripts/discourse/app/lib/plugin-api.gjs)

### Community Resources

- [Discourse Meta](https://meta.discourse.org/)
- [Theme Showcase](https://meta.discourse.org/c/theme/)
- [Plugin Outlets](https://meta.discourse.org/t/plugin-outlet-locations-theme-component/100673)

### Tools

- [Discourse Theme CLI](https://meta.discourse.org/t/discourse-theme-cli/82950)
- [Browser DevTools](https://developer.chrome.com/docs/devtools/)

## Getting Help

1. **Check Documentation**: Read this guide and official docs
2. **Search Meta**: Someone may have had the same issue
3. **Ask on Meta**: Post in the [dev category](https://meta.discourse.org/c/dev/)
4. **GitHub Issues**: Report bugs or request features

---

Happy theming! 🎨
