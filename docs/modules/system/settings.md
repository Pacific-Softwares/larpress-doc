# Settings

Configure global application settings through the admin panel. Access settings via **Admin Panel → System → Settings**.

All settings are organized into themed tabs for easy navigation and management.

## General Tab

### Site Information

Configure your site's basic information and branding:

- **Site Name** (Required) - Your website's name
- **Tagline** - A short tagline describing your site
- **Site Description** - Brief description used for SEO meta description
- **Keywords** - SEO keywords separated by commas
- **Site Author** - Name of the site author or organization
- **Footer Text** - Text displayed in the website footer
- **Logo Height** - Logo height in rem units (default: 3)
- **Admin Logo Height** - Logo height in admin panel in rem units (default: 3)
- **Logo** - Upload your site logo (PNG with transparent background recommended, max 2MB)
- **Favicon** - Upload your site favicon (32x32 or 16x16 PNG/ICO recommended, max 2MB)

## Contact Tab

### Contact Information

Manage your site's contact details:

- **Email** - Contact email address
- **Phone** - Contact phone number
- **Address** - Street address
- **City** - City name
- **State/Province** - State or province
- **ZIP/Postal Code** - Postal code
- **Country** - Select from a comprehensive list of countries

## Third Party Credentials Tab

### Social Login Configuration

Configure OAuth providers for social login:

**Google Login:**
- **Enable Google Login** - Toggle to enable/disable
- **Google Client ID** - Required when enabled
- **Google Client Secret** - Required when enabled

**Facebook Login:**
- **Enable Facebook Login** - Toggle to enable/disable
- **Facebook App ID** - Required when enabled
- **Facebook App Secret** - Required when enabled

**GitHub Login:**
- **Enable GitHub Login** - Toggle to enable/disable
- **GitHub Client ID** - Required when enabled
- **GitHub Client Secret** - Required when enabled

**LinkedIn Login:**
- **Enable LinkedIn Login** - Toggle to enable/disable
- **LinkedIn Client ID** - Required when enabled
- **LinkedIn Client Secret** - Required when enabled

### Google reCAPTCHA Configuration

Protect forms with Google reCAPTCHA:

- **Enable Google reCAPTCHA** - Toggle to enable/disable
- **reCAPTCHA Site Key** - Public key for frontend forms (required when enabled)
- **reCAPTCHA Secret Key** - Private key for server-side verification (required when enabled)

reCAPTCHA can be used on login, registration, contact forms, and other forms throughout the application.

## Social Media Tab

### Social Media Links

Add your social media profiles. You can enter full URLs or usernames:

- **Facebook** - Full URL (e.g., `https://facebook.com/yourpage`) or username (e.g., `@yourpage`)
- **Twitter/X** - Full URL or username
- **Instagram** - Full URL or username
- **LinkedIn** - Full URL or username
- **YouTube** - Full URL or channel name
- **GitHub** - Full URL or username
- **TikTok** - Full URL or username
- **Pinterest** - Full URL or username

## SEO Tab

### Analytics & Tracking

Configure analytics and tracking services:

- **Google Analytics ID** - Your Google Analytics tracking ID (e.g., `G-XXXXXXXXXX`)
- **Google Tag Manager ID** - Your GTM container ID (e.g., `GTM-XXXXXXX`)
- **Facebook Pixel ID** - Your Facebook Pixel ID
- **Default Robots Meta** - Choose default robots meta tag:
  - Index, Follow
  - Index, No Follow
  - No Index, Follow
  - No Index, No Follow

### robots.txt

- **robots.txt Content** - Edit your robots.txt file content directly from the admin panel. Changes are saved to both the database and the physical `robots.txt` file in the public directory.

## System Tab

### System Settings

Configure core system behavior:

- **Maintenance Mode** - Enable to prevent public access to your site
- **Maintenance Message** - Custom message displayed during maintenance (visible when maintenance mode is enabled)
- **Allow Registration** - Toggle to allow/disallow new user registrations
- **Require Email Verification** - Toggle to require email verification for new users
- **Default User Role** - Select the default role assigned to new users
- **Timezone** - Select your application timezone (searchable list with UTC offsets)
- **Date Format** - Choose date format:
  - `Y-m-d` (2024-01-15)
  - `m/d/Y` (01/15/2024)
  - `d/m/Y` (15/01/2024)
  - `d-m-Y` (15-01-2024)
  - `M d, Y` (Jan 15, 2024)
  - `F d, Y` (January 15, 2024)
  - `D, M d, Y` (Mon, Jan 15, 2024)
  - `l, F d, Y` (Monday, January 15, 2024)
- **Time Format** - Choose time format:
  - `H:i:s` (24-hour with seconds) - 14:30:45
  - `H:i` (24-hour) - 14:30
  - `h:i:s A` (12-hour with seconds) - 02:30:45 PM
  - `h:i A` (12-hour) - 02:30 PM
  - `g:i A` (12-hour, no leading zero) - 2:30 PM
  - `G:i` (24-hour, no leading zero) - 14:30

### Security Settings

Configure authentication and security:

- **Session Timeout (minutes)** - Number of minutes before a user session expires due to inactivity (default: 120)
- **Max Login Attempts** - Maximum failed login attempts before account lockout (default: 5)
- **Lockout Duration (minutes)** - Number of minutes an account is locked after max login attempts (default: 30)
- **Force HTTPS** - Redirect all HTTP traffic to HTTPS for enhanced security
- **Require Two-Factor Authentication** - Require all users to enable 2FA for their accounts

### Password Policy

Configure password requirements:

- **Minimum Password Length** - Minimum number of characters required (default: 8)
- **Require Uppercase Letters** - Passwords must contain at least one uppercase letter (A-Z)
- **Require Lowercase Letters** - Passwords must contain at least one lowercase letter (a-z)
- **Require Numbers** - Passwords must contain at least one number (0-9)
- **Require Special Characters** - Passwords must contain at least one special character (@$!%*?&#)

## Languages Tab

### Language Settings

Configure multi-language support:

- **Enable Multi Languages** - Toggle to enable multi-language functionality
- **Default Language** - Select the default language for your application (visible when multi-languages is enabled)

## Legal & Compliance Tab

### Legal Pages

Configure links to legal and policy pages:

- **Terms of Service URL** - URL to your Terms of Service page
- **Privacy Policy URL** - URL to your Privacy Policy page

### GDPR & Compliance

Configure GDPR and data protection settings:

- **Require Cookie Consent** - Display cookie consent banner to comply with GDPR and cookie laws
- **Enable GDPR Compliance** - Enable GDPR compliance features (data export, right to be forgotten, etc.)
- **Data Retention Period (days)** - Number of days to retain user data before automatic deletion (default: 365, visible when GDPR compliance is enabled)

## Email Tab

### Email Configuration

Configure SMTP settings for sending emails:

- **SMTP Host** - Your SMTP server hostname (e.g., `smtp.gmail.com`)
- **SMTP Port** - SMTP port number (commonly 587 for TLS, 465 for SSL, 25 for unencrypted)
- **Encryption** - Encryption method (TLS, SSL, or None)
- **SMTP Username** - Your SMTP username (usually your email address)
- **SMTP Password** - Your SMTP password or app-specific password
- **From Email Address** - Default sender email address
- **From Name** - Default sender name

### Test Email

Send a test email to verify your configuration:

- **Recipient Email** - Email address to send test email to
- **Test Message** - Message content for the test email
- **Send Test Email** - Button to send the test email (requires confirmation)

::: tip
Email settings configured here automatically update your `.env` file. Changes take effect immediately after saving.
:::

## SMS Tab

### Twilio SMS Configuration

Configure Twilio settings for sending SMS messages:

- **Twilio Account SID** - Your Twilio Account SID from the Twilio Console
- **Twilio Auth Token** - Your Twilio Auth Token from the Twilio Console
- **Twilio Phone Number** - Your Twilio phone number (must include country code, e.g., +1)

### Test SMS

Send a test SMS to verify your Twilio configuration:

- **Recipient Phone Number** - Phone number to send test SMS to (include country code)
- **Test Message** - Message content for the test SMS
- **Send Test SMS** - Button to send the test SMS (requires confirmation)

## Filesystem Tab

### Filesystem Settings

Configure file storage:

- **Filesystem Disk** - Select the default filesystem disk:
  - **Local** - Store files locally
  - **Public** - Store files in public directory
  - **Amazon S3** - Store files on Amazon S3

### Amazon S3 Configuration

When S3 is selected as the filesystem disk, configure AWS credentials:

- **AWS Access Key ID** (Required) - Your AWS access key
- **AWS Secret Access Key** (Required) - Your AWS secret key
- **AWS Default Region** (Required) - AWS region where your S3 bucket is located (e.g., `us-east-1`, `eu-north-1`)
- **AWS Bucket** (Required) - Your S3 bucket name
- **AWS Endpoint** (Optional) - S3 endpoint URL
- **AWS URL** (Optional) - Public URL for accessing files
- **Use Path Style Endpoint** - Enable if using path-style endpoint (required for some S3-compatible services)

::: tip
Filesystem settings configured here automatically update your `.env` file. Changes take effect immediately after saving.
:::

## How Settings Work

### Saving Settings

- All settings are saved to the `settings` database table
- Settings are cached for performance
- Cache is automatically cleared when settings are updated
- Email, filesystem, and AWS settings also update the `.env` file automatically
- Maintenance mode state is cached separately for quick access

### Accessing Settings in Code

Settings can be accessed using the `Setting` model:

```php
use App\Models\Setting;

// Get a setting value
$siteName = Setting::get('site_name', 'Default Value');

// Settings are automatically cached
// Cache key format: "setting.{key}"
```

### Environment Variables

Some settings automatically update environment variables:
- Filesystem disk settings (`FILESYSTEM_DISK`, `AWS_*`)
- Email settings (`MAIL_*`)

These changes are written to the `.env` file and take effect immediately after saving.

## Best Practices

1. **Test Email Configuration** - Always use the test email feature to verify SMTP settings before going live
2. **Security Settings** - Configure appropriate session timeout and login attempt limits for your use case
3. **Password Policy** - Set strong password requirements based on your security needs
4. **Maintenance Mode** - Use maintenance mode when performing updates or major changes
5. **SEO Settings** - Fill in analytics IDs and configure robots meta for better search engine visibility
6. **Filesystem** - Choose the appropriate storage disk based on your hosting and scalability needs
7. **Timezone** - Set the correct timezone to ensure accurate date/time displays
8. **GDPR Compliance** - Enable GDPR features if you serve users in the European Union

## Tips

- Settings are organized into logical tabs for easy navigation
- Most settings have helpful tooltips explaining their purpose
- Required fields are clearly marked
- Conditional fields appear/disappear based on toggle selections
- Test features (email/SMS) help verify configurations before going live
- All file uploads respect the configured filesystem disk setting
