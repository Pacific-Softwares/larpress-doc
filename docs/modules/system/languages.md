# Languages

Manage available locales and translation files through the admin panel. Access language management via **Admin Panel → System → Languages**.

## Overview

The Languages module allows you to:
- Add new languages to your application
- Configure language settings (name, code, RTL support)
- Edit translation files for each language
- Manage which languages are available to users

## Creating a Language

To add a new language:

1. Navigate to **Admin Panel → System → Languages**
2. Click **Create Language** or **New Language**
3. Fill in the language details:

### Language Information

- **Language Name** (Required) - The display name of the language (e.g., "Spanish", "French", "Arabic")
  - Must be unique
  - Cannot be edited for the English language
  
- **Language Code** (Required) - The ISO language code (e.g., `es`, `fr`, `ar`)
  - Must be unique
  - Typically follows ISO 639-1 standard (two-letter codes)
  - Cannot be edited for the English language

- **RTL** (Toggle) - Enable this for right-to-left languages (e.g., Arabic, Hebrew, Urdu)
  - When enabled, the interface will automatically switch to RTL layout
  - Cannot be changed for the English language

4. Click **Save** to create the language

## Managing Languages

### Language List

The language list displays all available languages with the following information:

- **Name** - Language display name (searchable and sortable)
- **Code** - Language code (sortable)
- **RTL** - Shows "Yes" or "No" badge indicating if RTL is enabled
  - Green badge indicates RTL is enabled
  - Gray badge indicates LTR (left-to-right)

### Language Actions

Each language (except English) has the following actions available:

- **Edit** - Modify language name, code, and RTL settings
- **Edit Files** - Open the translation file editor to manage translations for this language
- **Delete** - Remove the language from the system

### Protected Language

The **English** language (code: `en`) is protected and cannot be:
- Edited (name, code, or RTL settings are locked)
- Deleted
- Modified in any way

This ensures that English always remains available as a fallback language.

## Editing Translation Files

To edit translation files for a language:

1. Navigate to **Admin Panel → System → Languages**
2. Find the language you want to edit
3. Click **Edit Files** action button
4. The translation file editor will open, allowing you to:
   - View all translation keys
   - Edit translation values
   - Add new translations
   - Search for specific translations

## Language Code Standards

When adding languages, use standard ISO 639-1 language codes:

- `en` - English
- `es` - Spanish
- `fr` - French
- `de` - German
- `it` - Italian
- `pt` - Portuguese
- `ar` - Arabic
- `zh` - Chinese
- `ja` - Japanese
- `ko` - Korean
- `ru` - Russian
- `hi` - Hindi
- `tr` - Turkish
- And more...

::: tip
For a complete list of ISO 639-1 language codes, refer to the [ISO 639-1 standard](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).
:::

## RTL (Right-to-Left) Languages

Languages that read from right to left should have the RTL toggle enabled. Common RTL languages include:

- Arabic (`ar`)
- Hebrew (`he`)
- Urdu (`ur`)
- Persian/Farsi (`fa`)
- Kurdish (`ku`)

When RTL is enabled:
- The interface automatically flips the layout direction
- Text alignment changes to right-aligned
- Navigation and UI elements are mirrored
- Forms and inputs adapt to RTL layout

## Best Practices

1. **Use Standard Codes** - Always use ISO 639-1 two-letter language codes for consistency
2. **Enable RTL Correctly** - Only enable RTL for languages that actually read right-to-left
3. **Keep English** - Never delete or modify the English language as it serves as the base language
4. **Test Translations** - After adding a language, test the translation files to ensure everything displays correctly
5. **Complete Translations** - Make sure to translate all necessary strings for a complete user experience
6. **Language Names** - Use the native name of the language for better user recognition

## Integration with Settings

Language settings are integrated with the main Settings page:

- Enable/disable multi-language functionality in **Settings → Languages**
- Set the default language in **Settings → Languages → Default Language**
- The default language must be enabled in multi-language settings

## Tips

- Language codes should be lowercase and follow ISO standards
- RTL support is automatically handled by the system when enabled
- Translation files are organized by language code in the `lang/` directory
- You can have multiple languages active simultaneously
- Users can switch between languages if multi-language is enabled in settings
- The "Edit Files" action is the primary way to manage translations after creating a language
