# Hoojah Theme for Discourse

A fork of Fakebook theme for Discourse.

> ⚠️ **COMPATIBILITY NOTICE**: This theme is currently compatible with Discourse 2.6.x - 2.9.x only.
> It requires significant updates to work with Discourse 3.x. See [MODERNIZATION_NOTES.md](MODERNIZATION_NOTES.md) for details.

## What is Hoojah?

Hoojah is an online ecosystem for Malaysians to engage in thoughtful discussions, understand different points of view, and help with collaborative decision-making.

The Hoojah ecosystem comprises of these main principles:

- Transparency through open source technologies and democratic decision making
- Help Malaysia catch up with the rest of the world in the effort to digitalise everyday life by building tools to enable people to connect and local businesses grow.
- Educate Malaysians to normalise making data driven decisions

The Hoojah ecosystem has four main layers:

- Hoojah:**Borak** - social messaging app based on Telegram
- Hoojah:**Bincang** - community platform based on Discourse
- Hoojah:**BalaiRaya** - a dedicated platform for big issues discussions.
- Hoojah:**Bina** - API services to integrate other applications or services with Hoojah

This repository will host the theme for Hoojah:Bincang.

## Features

- **Facebook-style Topic List**: Card-based layout with avatars, excerpts, and engagement metrics
- **Custom Sidebar Widget**: Shows user stats, badges, and welcome messages
- **Hoojah Brand Colors**: Custom color scheme matching Hoojah identity
- **Responsive Design**: Optimized for both desktop and mobile viewing
- **Configurable Settings**: Toggle sidebar elements via theme settings

## Installation

### For Discourse 2.6.x - 2.9.x

1. Go to your Discourse Admin panel
2. Navigate to **Customize → Themes**
3. Click **Install** and choose **From a git repository**
4. Enter the repository URL: `https://github.com/hoojah/hoojah-discourse-theme.git`
5. Click **Install**

### For Discourse 3.x+

**This theme is not yet compatible with Discourse 3.x.** Major refactoring is required due to:
- Removal of raw Handlebars template support (.hbr files)
- Complete rewrite of topic-list architecture
- Migration to Glimmer components (.gjs format)

See [MODERNIZATION_NOTES.md](MODERNIZATION_NOTES.md) for detailed migration requirements.

## Configuration

After installation, you can configure the theme in **Admin → Customize → Themes → Hoojah Theme → Edit CSS/HTML**:

### Available Settings

- `sidebar_alignment`: Position sidebar on left or right (default: left)
- `sidebar_show_intro`: Show/hide welcome message (default: true)
- `sidebar_show_likes`: Show/hide likes statistics (default: true)
- `sidebar_show_badges`: Show/hide user badges (default: true)

## Development Status

### Current Version (Phase 1 - January 2025)

✅ Compatibility markers updated
✅ Plugin API version updated to 1.14
✅ Deprecation warnings added to code
✅ Documentation for breaking changes created

### Roadmap

**Phase 2 - Discourse 3.x Compatibility** (Not yet started)
- [ ] Convert .hbr templates to .gjs Glimmer components
- [ ] Rewrite topic list customization using new APIs
- [ ] Update sidebar widget to modern patterns
- [ ] Replace modifyClass with plugin outlets/transformers
- [ ] Comprehensive testing on Discourse 3.5.x

**Phase 3 - Optimization** (Future)
- [ ] Performance improvements
- [ ] Enhanced mobile experience
- [ ] Additional customization options
- [ ] Automated testing

## Technical Details

### Technologies Used
- SCSS (styling)
- JavaScript (Discourse Plugin API 1.14)
- Handlebars templates (deprecated, needs migration to .gjs)
- CSS Grid for responsive layout

### Browser Support
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile browsers on iOS 16.7+ and Android

### Known Issues
- ⚠️ Uses deprecated raw template system (.hbr files)
- ⚠️ Uses `modifyClass` which is discouraged
- ⚠️ Not compatible with Discourse 3.x without major refactor

See [MODERNIZATION_NOTES.md](MODERNIZATION_NOTES.md) for complete technical details.

## Contributing

We welcome contributions! If you'd like to help modernize this theme for Discourse 3.x:

1. Review [MODERNIZATION_NOTES.md](MODERNIZATION_NOTES.md) for technical requirements
2. Fork the repository
3. Create a feature branch
4. Make your changes
5. Submit a pull request

Priority areas:
- Converting .hbr templates to .gjs format
- Implementing new topic-list customization APIs
- Testing on Discourse 3.x instances

## Support

For issues and questions:
- Check [MODERNIZATION_NOTES.md](MODERNIZATION_NOTES.md) for known issues
- Open an issue on GitHub
- Visit [Discourse Meta](https://meta.discourse.org/) for Discourse development help

## License

GNU General Public License v2.0 - see [LICENSE](LICENSE) file for details.

## Credits

- Original **Fakebook** theme by the Discourse community
- Adapted for **Hoojah** by the Hoojah team
- Maintained for Malaysian community engagement

---

**Last Updated**: January 2025
**Discourse Compatibility**: 2.6.x - 2.9.x
**Status**: Legacy (Phase 2 modernization needed for 3.x)
