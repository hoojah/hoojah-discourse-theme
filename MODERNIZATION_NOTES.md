# Hoojah Discourse Theme - Modernization Notes

## Current Status (January 2025)

This theme was originally developed for Discourse 2.6.0.beta3 and requires significant updates to work with modern Discourse (3.5.x+).

## Critical Deprecations Found

### 1. Raw Handlebars Templates (.hbr) - **DEPRECATED**

**Status**: No longer supported in Discourse 3.x
**Impact**: HIGH - Core functionality broken

**Affected Files**:
- `javascripts/discourse/templates/topic-list-header.hbr`
- `javascripts/discourse/templates/list/custom-topic-list-item.hbr`
- `javascripts/discourse/templates/list/posts-count-column.hbr`

**What needs to happen**:
- Raw templates (.hbr) have been replaced with Glimmer components (.gjs)
- The topic-list has been completely rewritten using modern Glimmer architecture
- Custom topic list rendering requires using new plugin outlets and transformers

**Migration Path**:
1. Remove `.hbr` template overrides
2. Use the new topic-list plugin outlets and transformers API
3. Consider using `api.renderInOutlet()` or similar modern approaches
4. Convert templates to .gjs format if creating custom components

**Resources**:
- [Upcoming topic-list changes](https://meta.discourse.org/t/upcoming-topic-list-changes-how-to-prepare-themes-and-plugins/343404)
- [.gjs format migration](https://meta.discourse.org/t/automatically-updating-themes-and-plugins-to-gjs-file-format/368051)

### 2. modifyClass Usage - **DISCOURAGED**

**Status**: Should be last resort
**Impact**: MEDIUM - May break with Discourse updates

**Affected Files**:
- `common/header.html` (line 4-11)

**Current Usage**:
```javascript
api.modifyClass('component:topic-list-item', {
  renderTopicListItem() {
    const template = findRawTemplate("list/custom-topic-list-item");
    if (template) {
      this.set("topicListItemContents", template(this).htmlSafe());
    }
  },
});
```

**Issues**:
- `modifyClass` is unstable and can break with core updates
- Used in conjunction with deprecated raw templates
- Topic list architecture has completely changed

**Recommended Alternatives** (in order of preference):
1. Plugin Outlets - Use existing discourse outlets
2. Transformers API - New in 2025 for customizing client behavior
3. Plugin API methods - Specialized methods for common customizations
4. modifyClass with pluginId - Only as last resort with proper identification

**Resources**:
- [Using Transformers](https://meta.discourse.org/t/using-transformers-to-customize-client-side-values-and-behavior/349954)
- [modifyClass best practices](https://meta.discourse.org/t/using-modifyclass-to-change-core-behavior/262064)

### 3. Old Plugin API Version

**Status**: Outdated
**Impact**: LOW - Still works but limits access to new features

**Current**: `version="0.8"`
**Recommended**: `version="1.14"` (or latest)

### 4. Connector Class Pattern - Partially Outdated

**Affected Files**:
- `desktop/header.html` (sidebar connector)

**Current Pattern**: Works but may need updates for modern Discourse
**Consideration**: The `discovery-below` outlet may have changed or better alternatives exist

## Updated Compatibility Requirements

### Discourse Version Support
- **Current**: 2.6.0.beta3 (very old)
- **Target**: 3.5.0+ (latest stable)
- **Minimum Recommended**: 3.1.0

### Browser Requirements (2025)
- Safari on iOS 16.7+
- Latest stable releases of major browsers
- Modern JavaScript features available

### Server Requirements
- Ruby 3.3+
- PostgreSQL 13+
- Redis 7+

## SCSS/Styling - Status: OK

The SCSS appears to be using standard CSS that should remain compatible with Discourse 3.x:
- Uses standard CSS Grid and Flexbox
- Uses Discourse SCSS variables properly
- No deprecated CSS detected

**Minor updates recommended**:
- Review any changes to Discourse's CSS class names
- Test with modern Discourse UI components

## Breaking Changes Summary

### High Priority (Breaks Theme)
1. ❌ Raw template system completely removed
2. ❌ Topic-list architecture completely rewritten
3. ❌ Old component override methods no longer work

### Medium Priority (May Break)
1. ⚠️ `modifyClass` may break with core updates
2. ⚠️ Plugin outlets may have changed
3. ⚠️ Connector patterns may need updates

### Low Priority (Works but Outdated)
1. ℹ️ Plugin API version outdated
2. ℹ️ Compatibility file format can be improved

## Recommended Modernization Strategy

### Phase 1: Immediate Updates (Safe)
- [x] Update `.discourse-compatibility` file
- [x] Update plugin API version to 1.14+
- [x] Add `minimum_discourse_version` to `about.json`
- [x] Add deprecation warnings in comments
- [x] Document breaking changes

### Phase 2: Major Refactor (Required for Discourse 3.x)
- [ ] Remove `.hbr` template overrides
- [ ] Research new topic-list customization APIs
- [ ] Rewrite topic list customization using plugin outlets/transformers
- [ ] Convert custom components to .gjs format
- [ ] Update sidebar widget to use modern patterns
- [ ] Test on Discourse 3.5.x instance

### Phase 3: Optimization
- [ ] Replace `modifyClass` with stable APIs where possible
- [ ] Add error handling for missing APIs
- [ ] Improve mobile responsiveness
- [ ] Add comprehensive testing

## Technical Debt

1. **Custom Topic List**: The Facebook-style card layout is the core feature but uses completely deprecated APIs. This is the biggest technical debt item.

2. **Sidebar Widget**: Uses older connector pattern. Should be reviewed for modern equivalents.

3. **Template Overrides**: All `.hbr` files need to be converted or removed.

## Testing Requirements

Before deployment to production:
1. Test on Discourse 3.5.x staging instance
2. Verify topic list displays correctly
3. Verify sidebar widget loads and displays data
4. Test mobile responsiveness
5. Check browser console for errors
6. Test with both logged-in and anonymous users
7. Verify all theme settings work correctly

## Migration Timeline Estimate

- **Phase 1**: 1-2 hours (compatibility updates, documentation)
- **Phase 2**: 8-16 hours (major refactor, testing)
- **Phase 3**: 4-8 hours (optimization, final testing)

**Total**: 13-26 hours of development work

## Current Status After Updates

✅ Compatibility files updated
✅ Plugin API version updated
✅ Deprecation warnings added
✅ Documentation created
⚠️ Core functionality still needs major refactor for Discourse 3.x
⚠️ Theme may not work correctly on Discourse 3.x without Phase 2 work

## Immediate Next Steps

1. Deploy Phase 1 updates to track compatibility
2. Set up Discourse 3.5.x staging environment
3. Research new topic-list customization APIs
4. Begin Phase 2 refactor with new APIs
5. Test thoroughly before production deployment

## Additional Resources

- [Discourse Developer Docs](https://github.com/discourse/discourse-developer-docs)
- [Theme Development Guide](https://meta.discourse.org/t/developing-discourse-themes-theme-components/93648)
- [Plugin API Documentation](https://github.com/discourse/discourse/blob/main/app/assets/javascripts/discourse/app/lib/plugin-api.gjs)
- [Discourse Meta - Developer Category](https://meta.discourse.org/c/dev/)

---

*Last Updated: January 2025*
*Discourse Target Version: 3.5.2*
