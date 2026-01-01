# Sliders

Create hero sliders with buttons, media, and status controls.

## Form highlights
- Heading/subheading fields plus two optional CTA buttons
- Order field, background color, and percentage slider for layout tuning
- Upload an image or video (up to 50 MB) and toggle active state

## Table tools
- Searchable headings with active/inactive icon column
- Quick edit/delete actions and bulk removal

## Translations

If multi-language support is enabled (via **Admin Panel → Settings → Languages → Enable Multi Languages**), you can add translations for slider content in different languages.

### Accessing Translations

1. Navigate to **Admin Panel → Content → Sliders**
2. Edit an existing slider
3. Click the **Manage Translations** button in the header actions
4. The translation modal will open with tabs for each available language

### Translatable Fields

The following fields can be translated:

- **Heading** - Translated slider heading/title
- **Subheading** - Translated slider subheading/description
- **First Button Name** - Translated label for the first call-to-action button
- **Second Button Name** - Translated label for the second call-to-action button

### Translation Interface

The translation modal provides:

- **Language Tabs** - One tab for each enabled language (English is the default language)
- **Completion Badge** - A checkmark (✓) badge appears on language tabs when the heading translation exists (heading is the primary field)
- **Form Fields** - Input fields for heading, subheading, and button names in the selected language
- **Auto-save** - Translations are saved when you submit the form

### How It Works

- English is the default language and cannot be translated (it serves as the base)
- Translations are stored separately in the `translations` table
- Each translation is linked to the slider record via `translatable_type` and `translatable_id`
- When viewing sliders in a specific language, the system automatically retrieves the appropriate translation
- If a translation doesn't exist, the system falls back to the English version
- Slider media (images/videos), layout settings, and button URLs remain the same across languages; only text content is translated

### Best Practices for Translations

1. **Translate All Text** - Translate heading, subheading, and button labels for a complete localized experience
2. **Button Labels** - Ensure button labels are clear and actionable in each language
3. **Check Completion** - Use the checkmark badge to quickly identify which languages need translations
4. **CTA Consistency** - Maintain consistent call-to-action messaging across languages while adapting to cultural preferences
5. **Length Considerations** - Consider that translations may be longer or shorter than the English version; test slider layout in each language
