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
- **Icon** (Optional) - Icon identifier for the content.
- **Content Type** (Required) - Select from available content types (e.g., Page, Post, Article).
- **Content Type Category** (Optional) - Organize content into categories.
- **Layout** (Required) - Choose from active theme layouts.
- **Order Number** - Numeric value for sorting/ordering content.
- **Popular** - Toggle to mark content as popular/featured.
- **Reference/External URL** (Optional) - Link to external resources.
- **Thumbnail Image** - Upload a thumbnail image for the content.
- **Banner Image** - Upload a banner image for the content.

### Content Section

- **Short Description** - Brief summary of the content.
- **Description** - Rich text editor for main content with support for:
  - Bold, italic, underline
  - Bullet and numbered lists
  - Links
  - Code blocks
  - HTML block shortcodes: `[[slug-of-html-block]]`

::: tip Shortcodes
You can insert reusable HTML blocks into your content using shortcodes:
```
[[slug-of-html-block]]
```
This will be replaced with the content of the HTML block matching that slug.
:::

### Status & Meta Section

**Status Options:**
- **Draft** - Content is saved but not visible to the public.
- **Published** - Content is live and visible.
- **Scheduled** - Content will be published at a specific date/time.

When selecting "Scheduled" status:
- **Scheduled Date** - Set the date and time when content should become visible.

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
- **Search** - Search by title.
- **Filters** - Filter by status (Draft, Published, Scheduled).
- **Columns**:
  - Title (searchable, sortable)
  - Slug (copyable)
  - Type (badge)
  - Status (color-coded badge)
  - Updated date

### Bulk Actions

- **Bulk Delete** - Select multiple items and delete them at once.

### Content Status

Content can have three statuses:

1. **Draft** - Not visible to public
2. **Published** - Live and visible
3. **Scheduled** - Will be published automatically at the scheduled date/time

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

## Best Practices

1. **Consistent Layouts** - Keep layouts consistent with the selected content type.
2. **SEO Optimization** - Always fill in meta title, description, and keywords for better search engine visibility.
3. **Use Categories** - Organize related content using categories.
4. **Scheduled Publishing** - Use scheduled status for time-sensitive content.
5. **HTML Blocks** - Create reusable HTML blocks and reference them via shortcodes for consistent design.
6. **Additional Data** - Use additional data fields for custom metadata that doesn't fit standard fields.
7. **Popular Flag** - Mark featured or important content as popular for easy filtering.

## Tips

- Slugs are auto-generated from titles but can be manually edited
- Each content type can have unique slugs (same slug can exist in different types)
- Use the order field to control display order when listing content
- Thumbnail and banner images are stored using the configured filesystem disk
- Rich editor supports HTML, so you can add custom markup if needed
