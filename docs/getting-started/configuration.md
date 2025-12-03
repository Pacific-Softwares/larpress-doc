# Configuration

Learn how to configure larpress for your specific needs.

## Environment Configuration

larpress uses Laravel's `.env` file for environment-specific configuration.

### Essential Settings

```env
# Application
APP_NAME="larpress"
APP_ENV=production
APP_KEY=base64:generated_key_here
APP_DEBUG=false
APP_URL=https://your-domain.com

# Database
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=larpress
DB_USERNAME=root
DB_PASSWORD=your_secure_password

# Cache
CACHE_DRIVER=redis
QUEUE_CONNECTION=redis
SESSION_DRIVER=redis

# Redis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

# Mail
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS="noreply@your-domain.com"
MAIL_FROM_NAME="${APP_NAME}"
```

## Database Configuration

### MySQL

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=larpress
DB_USERNAME=root
DB_PASSWORD=
```

### PostgreSQL

```env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=larpress
DB_USERNAME=postgres
DB_PASSWORD=
```

### SQLite (Development Only)

```env
DB_CONNECTION=sqlite
DB_DATABASE=/absolute/path/to/database.sqlite
```

## Cache Configuration

### Redis (Recommended for Production)

```bash
# Install Redis
sudo apt install redis-server

# Start Redis
sudo systemctl start redis
sudo systemctl enable redis
```

```env
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
```

### File Cache (Development)

```env
CACHE_DRIVER=file
SESSION_DRIVER=file
```

## Queue Configuration

### Redis Queue (Production)

```env
QUEUE_CONNECTION=redis
```

### Database Queue

```env
QUEUE_CONNECTION=database
```

Run queue worker:

```bash
php artisan queue:work --daemon
```

## File Storage

File storage settings can be configured from **Admin Panel → Settings → Filesystem** tab, or manually via `.env` file.

### Local Storage (Default)

```env
FILESYSTEM_DISK=local
```

Or configure via Admin Panel → Settings → Filesystem → Select "Local" as Filesystem Disk.

### Amazon S3

Configure via Admin Panel → Settings → Filesystem:
- Select "Amazon S3" as Filesystem Disk
- Enter your AWS credentials:
  - AWS Access Key ID
  - AWS Secret Access Key
  - AWS Default Region (e.g., `us-east-1`)
  - AWS Bucket name
  - (Optional) AWS Endpoint and URL

Alternatively, you can set these in `.env`:

```env
FILESYSTEM_DISK=s3
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=your-bucket-name
```

## Email Configuration

Email settings can be configured from **Admin Panel → Settings → Email** tab, or manually via `.env` file.

### Configure via Admin Panel

Navigate to **Admin Panel → Settings → Email** tab to configure:
- SMTP Host
- SMTP Port (commonly 587 for TLS, 465 for SSL, 25 for unencrypted)
- Encryption (TLS, SSL, or None)
- SMTP Username
- SMTP Password
- From Email Address
- From Name

The admin panel also includes a test email feature to verify your configuration.

### Configure via .env File

Alternatively, you can set these in `.env`:

```env
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your-email@gmail.com
MAIL_PASSWORD=your-app-password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS="noreply@your-domain.com"
MAIL_FROM_NAME="${APP_NAME}"
```

::: tip
Settings configured via the admin panel will automatically update your `.env` file. Changes take effect immediately after saving.
:::

## Application Settings

### Site Settings

Manage via Admin Panel → Settings:

- Site Name
- Site Description
- Logo & Favicon
- Contact Information
- Social Media Links
- SEO Settings
- Analytics Code

## Security Configuration

### IP Restrictions

Enable IP whitelist in Admin Panel → Access Control → IP Restrictions.

### API Rate Limiting

Configure in `config/larpress.php`:

```php
'api' => [
    'rate_limit' => 60, // requests per minute
    'throttle' => '60,1', // 60 requests per 1 minute
],
```

### Two-Factor Authentication

Enable in Admin Panel → Settings → Security:

```php
'security' => [
    '2fa_enabled' => true,
    'session_timeout' => 120, // minutes
    'password_expiry' => 90, // days
],
```

## Performance Optimization

### OPcache

Enable in `php.ini`:

```ini
opcache.enable=1
opcache.memory_consumption=256
opcache.max_accelerated_files=20000
opcache.validate_timestamps=0
```

### Application Optimization

```bash
# Cache everything
php artisan optimize

# Individual caches
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan event:cache
```

### Database Optimization

```bash
# Enable query caching
php artisan config:cache
```

## Debugging

### Enable Debug Mode

```env
APP_DEBUG=true
LOG_LEVEL=debug
```

## Localization

### Add Languages

Admin Panel → System → Languages


## Next Steps

- [Quick Start Guide](/getting-started/quick-start)
- [Module Development](/modules/introduction)
- [Theme Management](/modules/system/themes)

