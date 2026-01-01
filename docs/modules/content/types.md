# Types

Define reusable content types (e.g., Page, Post, Product) with status control.

## Form highlights
- Name and slug inputs with unique validation
- Active/inactive toggle for availability
- Optional description field for editorial notes
## Table tools
- Search or sort by name/slug and preview description
- Status badge indicates active/inactive state
- Quick edit/delete actions (core `page` type stays protected)

## Translations

If multi-language support is enabled (via **Admin Panel → Settings → Languages → Enable Multi Languages**), you can add translations for content types in different languages.

### Accessing Translations

1. Navigate to **Admin Panel → Content → Types**
2. Edit an existing content type
3. Click the **Manage Translations** button in the header actions
4. The translation modal will open with tabs for each available language

### Translatable Fields

The following fields can be translated:

- **Name** - Translated content type name
- **Description** - Translated description for the content type

### Translation Interface

The translation modal provides:

- **Language Tabs** - One tab for each enabled language (English is the default language)
- **Completion Badge** - A checkmark (✓) badge appears on language tabs when both name and description translations are complete
- **Form Fields** - Input fields for name and description in the selected language
- **Auto-save** - Translations are saved when you submit the form

### How It Works

- English is the default language and cannot be translated (it serves as the base)
- Translations are stored separately in the `translations` table
- Each translation is linked to the content type record via `translatable_type` and `translatable_id`
- When viewing content types in a specific language, the system automatically retrieves the appropriate translation
- If a translation doesn't exist, the system falls back to the English version

### Best Practices for Translations

1. **Complete All Fields** - Translate both name and description for consistency
2. **Use Appropriate Terms** - Ensure content type names are culturally appropriate in each language
3. **Check Completion** - Use the checkmark badge to quickly identify which languages need translations
4. **Keep Descriptions Clear** - Provide clear, descriptive translations that explain the content type's purpose
