# Hoojah Discourse Theme

A modern, clean theme for Discourse built with 2025 best practices.

## About Hoojah

Hoojah is an online ecosystem for Malaysians to engage in thoughtful discussions, understand different points of view, and help with collaborative decision-making.

The Hoojah ecosystem comprises these main principles:

- **Transparency** through open source technologies and democratic decision making
- **Digitalization** - Help Malaysia catch up with the rest of the world by building tools to connect people and grow local businesses
- **Data-driven decisions** - Educate Malaysians to normalize making data-driven decisions

### The Hoojah Ecosystem

- **Hoojah:Borak** - Social messaging app based on Telegram
- **Hoojah:Bincang** - Community platform based on Discourse (this theme)
- **Hoojah:BalaiRaya** - Platform for big issues discussions
- **Hoojah:Bina** - API services to integrate applications with Hoojah

## Features

✨ **Modern Architecture**
- Built with Discourse 3.x compatibility
- Uses latest Plugin API 1.14
- No deprecated patterns (no .hbr files)
- Modern Glimmer component approach

🎨 **Clean Design**
- Hoojah brand colors
- Responsive layout (mobile & desktop)
- Smooth animations and transitions
- Touch-optimized for mobile

⚙️ **Customizable**
- Theme settings for easy customization
- Custom logo upload
- Adjustable brand colors
- Wide layout option
- Custom CSS support

🚀 **Performance**
- Optimized CSS
- Modern best practices
- Minimal JavaScript
- Fast loading times

## Installation

### Requirements

- Discourse 3.1.0 or higher
- Admin access to your Discourse instance

### Install from Git Repository

1. Go to your Discourse Admin panel
2. Navigate to **Customize → Themes**
3. Click **Install** and choose **From a git repository**
4. Enter the repository URL:
   ```
   https://github.com/hoojah/hoojah-discourse-theme.git
   ```
5. Click **Install**
6. Set as default theme or make it selectable by users

### Manual Installation

1. Download this repository as a ZIP file
2. Go to **Admin → Customize → Themes**
3. Click **Install → From a file**
4. Upload the ZIP file
5. Configure and activate

## Configuration

After installation, configure the theme in **Admin → Customize → Themes → Hoojah → Settings**:

### Available Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `brand_logo` | Upload | - | Custom logo to replace default Discourse logo |
| `brand_color` | String | #415DE6 | Primary brand color (hex code) |
| `enable_custom_fonts` | Boolean | false | Enable custom font styling |
| `enable_wide_layout` | Boolean | false | Wider content layout for desktop |
| `custom_css` | Text | - | Add custom CSS to override styles |

### Color Scheme

The default Hoojah color scheme includes:

- **Primary**: #343A40 (Dark gray)
- **Tertiary**: #415DE6 (Hoojah blue)
- **Love**: #E1306C (Pink accent)
- **Secondary**: #FFFFFF (White)

You can customize these in **Admin → Customize → Colors**.

## Development

### Project Structure

```
hoojah-discourse-theme/
├── common/
│   ├── common.scss          # Shared styles
│   └── head_tag.html        # JavaScript & customizations
├── desktop/
│   └── desktop.scss         # Desktop-specific styles
├── mobile/
│   └── mobile.scss          # Mobile-specific styles
├── locales/
│   └── en.yml               # English translations
├── assets/
│   └── images/              # Theme images
├── about.json               # Theme metadata
├── settings.yml             # Theme settings definition
├── .discourse-compatibility # Version compatibility
├── .gitignore
├── LICENSE
└── README.md
```

### Building Components

This theme uses modern Discourse development practices:

#### Plugin API (v1.14)

Use the `withPluginApi` pattern for JavaScript customizations:

```javascript
const { withPluginApi } = require("discourse/lib/plugin-api");

withPluginApi("1.14", (api) => {
  // Your customizations here
});
```

#### Transformers

Use transformers for modifying values and behavior:

```javascript
api.registerValueTransformer("transformer-name", ({ value }) => {
  return modifiedValue;
});
```

#### Plugin Outlets

Inject content using plugin outlets:

```javascript
api.renderInOutlet("outlet-name", <template>
  <div>Your content</div>
</template>);
```

### Best Practices

1. **Use Plugin Outlets** over `modifyClass` when possible
2. **Use Transformers** for value modifications
3. **Avoid deprecated APIs** (raw templates, old patterns)
4. **Test on multiple devices** (desktop, mobile, tablet)
5. **Keep JavaScript minimal** for performance
6. **Use CSS variables** for theming
7. **Follow Discourse coding standards**

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/hoojah/hoojah-discourse-theme.git
   cd hoojah-discourse-theme
   ```

2. Install on your local Discourse instance via Admin UI

3. Make changes to files

4. Refresh your browser to see changes (Discourse auto-compiles)

5. Commit and push changes:
   ```bash
   git add .
   git commit -m "Description of changes"
   git push origin main
   ```

## Compatibility

- **Minimum Discourse Version**: 3.1.0
- **Tested On**: Discourse 3.5.x
- **Browser Support**:
  - Chrome (latest)
  - Firefox (latest)
  - Safari (latest)
  - Edge (latest)
  - Mobile browsers (iOS 16.7+, Android)

## Contributing

We welcome contributions! Here's how you can help:

1. **Report Issues**: Found a bug? [Open an issue](https://github.com/hoojah/hoojah-discourse-theme/issues)
2. **Suggest Features**: Have an idea? Share it in discussions
3. **Submit PRs**: Fork, make changes, and submit a pull request

### Contribution Guidelines

- Follow existing code style
- Test your changes thoroughly
- Update documentation as needed
- Keep commits focused and well-described
- Be respectful and collaborative

## Support

- **Documentation**: This README and code comments
- **Issues**: [GitHub Issues](https://github.com/hoojah/hoojah-discourse-theme/issues)
- **Discourse Meta**: [Developer Category](https://meta.discourse.org/c/dev/)
- **Community**: Join Hoojah:Bincang for discussions

## Roadmap

### Version 1.1 (Planned)
- [ ] Additional plugin outlet integrations
- [ ] More theme settings options
- [ ] Enhanced mobile experience
- [ ] Dark mode variant

### Version 1.2 (Future)
- [ ] Component library
- [ ] Advanced customization options
- [ ] Performance optimizations
- [ ] Accessibility improvements

## License

GNU General Public License v2.0

See [LICENSE](LICENSE) file for full details.

## Credits

- **Created by**: Hoojah Team
- **Maintained by**: Hoojah Community
- **Built for**: Malaysian thoughtful discourse
- **Powered by**: [Discourse](https://www.discourse.org/)

---

**Version**: 1.0.0
**Last Updated**: January 2025
**Discourse Compatibility**: 3.1.0+
**Status**: Active Development

Made with ❤️ for the Malaysian community
