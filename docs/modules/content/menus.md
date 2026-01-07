# Menus

Build hierarchical navigation menus with per-location settings.

![Menu Manager](/src/menu-manager.png)

## Form highlights
- Define name, parent, location, and URL/target options
- `is_base_url` toggle prepends the site URL automatically
- Configure icon, icon color, custom classes, order, active flag, permissions, and meta
## Table tools
- Displays breadcrumb-style menu path with location badges
- Copyable resolved URL, active icon, and sortable order column
- Filters by location, parent, and active state; supports bulk delete
- Drag to reorder via the table or open the tree view for full hierarchy

## Translations

If multi-language support is enabled (via **Admin Panel → Settings → Languages → Enable Multi Languages**), you can add translations for menu items in different languages.

### Accessing Translations

1. Navigate to **Admin Panel → Content → Menus**
2. Edit an existing menu item
3. Click the **Manage Translations** button in the header actions
4. The translation modal will open with tabs for each available language

### Translatable Fields

The following field can be translated:

- **Name** - Translated menu item name/label

### Translation Interface

The translation modal provides:

- **Language Tabs** - One tab for each enabled language (English is the default language)
- **Completion Badge** - A checkmark (✓) badge appears on language tabs when the name translation is complete
- **Form Fields** - Input field for the menu name in the selected language
- **Auto-save** - Translations are saved when you submit the form

### How It Works

- English is the default language and cannot be translated (it serves as the base)
- Translations are stored separately in the `translations` table
- Each translation is linked to the menu record via `translatable_type` and `translatable_id`
- When viewing menus in a specific language, the system automatically retrieves the appropriate translation
- If a translation doesn't exist, the system falls back to the English version
- Menu structure (parent-child relationships, URLs, icons) remains the same across languages; only the display name changes

### Best Practices for Translations

1. **Translate All Menu Items** - Ensure all menu items have translations for a complete localized navigation
2. **Keep URLs Consistent** - Menu URLs typically remain the same across languages, but menu labels should be translated
3. **Check Completion** - Use the checkmark badge to quickly identify which languages need translations
4. **Hierarchy Preservation** - Menu hierarchy and structure are preserved; only names are translated
5. **Cultural Considerations** - Consider cultural differences when translating menu labels (e.g., navigation structure preferences)
