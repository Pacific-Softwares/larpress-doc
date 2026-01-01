# Categories

Organize content types with active/inactive categories.

## Form highlights
- Name and slug inputs with uniqueness checks
- Status picker for active/inactive visibility
- Optional description field
## Table tools
- Searchable name/slug with optional description preview
- Status badges plus filters for status and parent content type
- Standard edit/delete actions with optional bulk removal

## Translations

If multi-language support is enabled (via **Admin Panel → Settings → Languages → Enable Multi Languages**), you can add translations for content type categories in different languages.

### Accessing Translations

1. Navigate to **Admin Panel → Content → Categories**
2. Edit an existing category
3. Click the **Manage Translations** button in the header actions
4. The translation modal will open with tabs for each available language

### Translatable Fields

The following fields can be translated:

- **Name** - Translated category name
- **Description** - Translated description for the category

### Translation Interface

The translation modal provides:

- **Language Tabs** - One tab for each enabled language (English is the default language)
- **Completion Badge** - A checkmark (✓) badge appears on language tabs when both name and description translations are complete
- **Form Fields** - Input fields for name and description in the selected language
- **Auto-save** - Translations are saved when you submit the form

### How It Works

- English is the default language and cannot be translated (it serves as the base)
- Translations are stored separately in the `translations` table
- Each translation is linked to the category record via `translatable_type` and `translatable_id`
- When viewing categories in a specific language, the system automatically retrieves the appropriate translation
- If a translation doesn't exist, the system falls back to the English version

### Best Practices for Translations

1. **Complete All Fields** - Translate both name and description for consistency
2. **Maintain Consistency** - Keep category names consistent across languages where appropriate
3. **Check Completion** - Use the checkmark badge to quickly identify which languages need translations
4. **Category Context** - Ensure category names and descriptions make sense within the content type context in each language
