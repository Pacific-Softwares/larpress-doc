# HTML Blocks

Reusable HTML snippets addressable by shortcode.

## Form highlights
- Auto-generate slug from title with unique validation
- Shows shortcode preview (`[[slug]]`) after save
- Large textarea for raw HTML/Blade content

## Table tools
- Copyable slug, searchable title, and updated timestamp
- Quick edit/delete actions with latest-first sorting

## Use cases
- Footers, banners, callouts, or marketing inserts
- Embed forms/widgets across multiple pages

## Translations

If multi-language support is enabled (via **Admin Panel → Settings → Languages → Enable Multi Languages**), you can add translations for HTML blocks in different languages.

### Accessing Translations

1. Navigate to **Admin Panel → Content → HTML Blocks**
2. Edit an existing HTML block
3. Click the **Manage Translations** button in the header actions
4. The translation modal will open with tabs for each available language

### Translatable Fields

The following fields can be translated:

- **Title** - Translated HTML block title
- **HTML Content** - Translated HTML content (can include full HTML markup)

### Translation Interface

The translation modal provides:

- **Language Tabs** - One tab for each enabled language (English is the default language)
- **Completion Badge** - A checkmark (✓) badge appears on language tabs when both title and content translations are complete
- **Form Fields** - Input fields for title and HTML content in the selected language
- **Auto-save** - Translations are saved when you submit the form

### How It Works

- English is the default language and cannot be translated (it serves as the base)
- Translations are stored separately in the `translations` table
- Each translation is linked to the HTML block record via `translatable_type` and `translatable_id`
- When viewing HTML blocks in a specific language, the system automatically retrieves the appropriate translation
- If a translation doesn't exist, the system falls back to the English version
- The HTML block slug remains the same across languages (same shortcode: `[[slug]]`), but the content changes based on the active language

### Best Practices for Translations

1. **Complete All Fields** - Translate both title and HTML content for consistency
2. **HTML Structure** - Maintain similar HTML structure across languages when possible, but adapt text content
3. **Check Completion** - Use the checkmark badge to quickly identify which languages need translations
4. **Content Adaptation** - Adapt HTML content to cultural preferences, not just direct translations
5. **Styling Consistency** - Ensure CSS classes and styling remain consistent across language versions
6. **Shortcode Usage** - Remember that the shortcode (`[[slug]]`) is the same for all languages; the system automatically shows the appropriate translation based on the current language
