# Content / Pages

Manage structured pages with type-aware layouts, media, and SEO metadata through the admin panel.

## Accessing Content Management

Navigate to **Admin Panel → Content → Content/Pages** to manage all your site's content and pages.

## Creating Content

### Basic Information

When creating or editing content, you'll find the following fields:

**Basic Info Section:**
- **Title** (Required) - The page title. The slug is auto-generated from the title but can be edited manually.
- **Slug** (Required) - URL-friendly identifier. Must be unique per content type.
- **Unique Code** - Auto-generated unique identifier for referencing content in code (read-only).
- **Content Type** (Required) - Select from available content types (e.g., Page, Post, Article).
- **Content Type Category** (Optional) - Organize content into categories.
- **Layout** (Required) - Choose from active theme layouts.
- **Content Width** - Select content width: Small, Medium, or Full (default: Full).
  - Note: Hero layout banner is always full width regardless of this setting.
- **Order Number** - Numeric value for sorting/ordering content.
- **Popular** - Toggle to mark content as popular/featured.
- **Show Related Page** - Toggle to show related content on the front detail page (default: enabled).
- **Show Left Sidebar** - Toggle to show left sidebar on the front detail page (default: disabled).
- **Show Right Sidebar** - Toggle to show right sidebar on the front detail page (default: disabled).
- **Show Comments** - Toggle to show comments section on the front detail page (default: disabled).
- **Thumbnail Image** - Upload a thumbnail image for the content.
- **Banner Image** - Upload a banner image for the content.
- **Gallery Images** - Upload multiple images for gallery layout. Images will be displayed in a grid with hover effects and click-to-preview functionality.

![Content Sidebar Options](/src/content-sidebar.png)

### Content Section

- **Short Description** - Brief summary of the content.
- **Description** - HTML code editor for main content. Insert full HTML here - it will be saved exactly as-is.
  - **Preview HTML** - Button to preview the HTML content in a new tab before saving.
  - Supports full HTML markup including custom CSS and JavaScript.

::: tip HTML Editor
The description field uses an HTML code editor, allowing you to write complete HTML markup. Use the "Preview HTML" button to see how your content will look before saving.
:::

### Status & Meta Section

**Status Options:**
- **Draft** - Work in progress, not visible on frontend (Gray badge).
- **Review** - Content is ready but awaiting approval (Orange badge).
- **Published** - Live on the website (Green badge).
- **Archived** - Old or retired content, kept for records (Muted badge).
- **Scheduled** - Will auto-publish in future (Purple badge).
- **Private** - Visible only to logged-in users (Red badge).

When selecting "Scheduled" status:
- **Scheduled Date** - Set the date and time when content should become visible (required, must be in the future).

**Published Date:**
- Automatically set when content is published or when scheduled content is published.
- Displayed as read-only information showing when the content was first published.

**SEO Settings:**
- **Meta Title** - SEO title (max 60 characters).
- **Meta Description** - SEO description (max 160 characters).
- **Meta Keywords** - Comma-separated keywords for SEO.

### Additional Data

Use the repeater field to add custom key-value pairs for additional metadata:
- **Label** - Field name/identifier.
- **Value** - Field content.

## Managing Content

### Content List View

The content list provides:
- **Search** - Search by title or unique code.
- **Filters**:
  - **Content Type** - Filter by one or more content types (multi-select, searchable).
  - **Category** - Filter by one or more categories (multi-select, searchable).
  - **Status** - Filter by status (multi-select): Draft, Review, Published, Archived, Scheduled, Private.
  - **Layout** - Filter by layout (multi-select, searchable).
  - **Popular/Featured** - Filter by popular flag (All, Popular only, Not popular).
- **Columns**:
  - Title (searchable, sortable)
  - Code (copyable, searchable, hidden by default)
  - Slug (copyable)
  - Type (badge showing content type name)
  - Status (color-coded badge with status name)
  - Updated date (sortable, default sort)

### Content Actions

Each content item has the following actions:

- **Preview** - View the content on the frontend in a new tab.
- **Duplicate** - Create a copy of the content with new content type and category selection.
  - Opens a modal to select:
    - New Content Type (required)
    - New Category (optional)
  - The duplicated content will have:
    - Title with " (Copy)" appended
    - New slug (auto-generated if conflict exists)
    - Status set to Draft
    - Published date reset
    - Scheduled date reset
    - All other content copied (description, images, meta, etc.)
  - After duplication, you'll be redirected to edit the new content.
- **Edit** - Modify the content.
- **Delete** - Remove the content from the system.

### Bulk Actions

- **Bulk Delete** - Select multiple items and delete them at once.

### Content Status

Content can have six statuses:

1. **Draft** (Gray) - Work in progress, not visible on frontend
2. **Review** (Orange) - Content is ready but awaiting approval
3. **Published** (Green) - Live on the website
4. **Archived** (Muted) - Old or retired content, kept for records
5. **Scheduled** (Purple) - Will auto-publish in future
6. **Private** (Red) - Visible only to logged-in users

Scheduled content automatically becomes published when the scheduled date/time is reached.

## Content Types

Content must be assigned to a content type. Content types define the structure and behavior of content. Create and manage content types from **Admin Panel → Content → Types**.

## Categories

Organize content using categories. Categories are optional but help with content organization. Manage categories from **Admin Panel → Content → Categories**.

## Using Content in Your Theme

### Helper Functions

The `ContentManagementHelper` class provides several methods for retrieving content:

**Get a single page by slug:**
```php
use App\Helpers\ContentManagementHelper;

$page = ContentManagementHelper::getPageBySlug('page', 'about');
// Returns Content model or null
```

**Get pages with filters:**
```php
$pages = ContentManagementHelper::getPages([
    'type' => 'post',        // Type slug or ID
    'status' => 'published',  // Status filter
    'category_id' => 1,       // Category ID
    'is_popular' => 1,        // Popular flag
], $perPage = 15, $search = null);
```

**Get published pages:**
```php
$publishedPages = ContentManagementHelper::getPublishedPages('post', $limit = 10);
```

**Get page by ID:**
```php
$page = ContentManagementHelper::getPageByID(1, 'published');
```

### Shortcode Parsing

Content descriptions automatically parse shortcodes:
- HTML Block shortcodes: `[[html-block-slug]]`
- Custom Form shortcodes: `[form:form-shortcode]`

Shortcodes are replaced when content is retrieved using the helper functions.

## Sidebar Configuration

Content pages support flexible sidebar layouts:

- **Left Sidebar** - Enable to show a left sidebar on the front detail page
- **Right Sidebar** - Enable to show a right sidebar on the front detail page
- **Both Sidebars** - You can enable both left and right sidebars simultaneously
- **Related Content** - Enable to show related content on the detail page
- **Comments** - Enable to show comments section on the detail page

Sidebar visibility is controlled per content item, allowing you to customize the layout for each page individually.

## Duplicating Content

The duplicate feature allows you to quickly create copies of existing content:

1. Click the **Duplicate** action button on any content item
2. Select the new **Content Type** (required)
3. Optionally select a new **Category**
4. Click **Duplicate**

The system will:
- Create a new content item with all data copied
- Append " (Copy)" to the title
- Generate a unique slug (adding numbers if needed)
- Set status to Draft
- Reset published and scheduled dates
- Redirect you to edit the new content

This is useful for:
- Creating variations of similar content
- Moving content between types
- Creating templates for future content
- Testing different layouts or categories

## Best Practices

1. **Consistent Layouts** - Keep layouts consistent with the selected content type.
2. **SEO Optimization** - Always fill in meta title, description, and keywords for better search engine visibility.
3. **Use Categories** - Organize related content using categories.
4. **Scheduled Publishing** - Use scheduled status for time-sensitive content.
5. **HTML Editor** - Use the HTML editor for full control over content markup and styling.
6. **Additional Data** - Use additional data fields for custom metadata that doesn't fit standard fields.
7. **Popular Flag** - Mark featured or important content as popular for easy filtering.
8. **Sidebar Configuration** - Configure sidebars per content item for flexible layouts.
9. **Content Duplication** - Use the duplicate feature to quickly create similar content.
10. **Unique Code** - Use the auto-generated unique code to reference content in your code.

## Translations

If multi-language support is enabled (via **Admin Panel → Settings → Languages → Enable Multi Languages**), you can add translations for content in different languages.

### Accessing Translations

1. Navigate to **Admin Panel → Content → Content/Pages**
2. Edit an existing content item
3. Click the **Manage Translations** button in the header actions
4. The translation modal will open with tabs for each available language

### Translatable Fields

The following fields can be translated:

- **Title** - Translated page title
- **Short Description** - Translated short description/summary
- **Description** - Translated full content description

### Translation Interface

The translation modal provides:

- **Language Tabs** - One tab for each enabled language (English is the default language)
- **Completion Badge** - A checkmark (✓) badge appears on language tabs when all required translations are complete
- **Form Fields** - Input fields for each translatable field in the selected language
- **Auto-save** - Translations are saved when you submit the form

### How It Works

- English is the default language and cannot be translated (it serves as the base)
- Translations are stored separately in the `translations` table
- Each translation is linked to the content record via `translatable_type` and `translatable_id`
- When viewing content in a specific language, the system automatically retrieves the appropriate translation
- If a translation doesn't exist, the system falls back to the English version

### Best Practices for Translations

1. **Complete All Fields** - Translate all fields (title, short description, description) for consistency
2. **Maintain Quality** - Ensure translations are accurate and culturally appropriate
3. **Check Completion** - Use the checkmark badge to quickly identify which languages need translations
4. **Review Regularly** - Periodically review translations to ensure they're up to date with content changes

## Tips

- Slugs are auto-generated from titles but can be manually edited
- Each content type can have unique slugs (same slug can exist in different types)
- Use the order field to control display order when listing content
- Thumbnail, banner, and gallery images are stored using the configured filesystem disk
- HTML editor allows full HTML markup - use the preview button to check your content
- Content width setting doesn't apply to Hero layout banners (they're always full width)
- Sidebar toggles allow flexible page layouts per content item
- Duplicate feature preserves all content data except status and dates
- Unique code is auto-generated and can be used to reference content programmatically
- Translations work independently - you can have different content for different languages while maintaining the same structure
- Status badges are color-coded for quick visual identification
