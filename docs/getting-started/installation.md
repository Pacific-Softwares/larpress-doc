# Installation

This guide will walk you through installing larpress on your server.

## Installation Methods

larpress offers multiple installation methods:

1. **Via File Manager (cPanel/Plesk/DirectAdmin)** – Upload ZIP, extract, then run installer
2. **Via FileZilla (FTP/SFTP)** – Upload ZIP, extract on server, then run installer
3. **Web Installer from Git/SSH** – Clone/checkout then run installer
4. **Manual Installation** – For advanced users and custom setups

---

## Method A: File Manager (cPanel/Plesk/DirectAdmin)

Use this when you have a hosting control panel with a browser File Manager.

1) Upload package
- Download the larpress release ZIP.
- In your panel, open File Manager and navigate to your target directory:
  - Root domain: `public_html/`
  - Subdomain/addon: that site’s document root
- Upload the ZIP to the target directory.

2) Extract files
- Use “Extract” in File Manager to unzip the archive into the target directory.

3) Install dependencies (Optional)
- The package already includes `vendor/` and pre-built npm assets, so this step is **optional**.
- If you want to update dependencies or rebuild assets, run these from the project root (SSH required):

```bash
composer install --no-dev --optimize-autoloader
npm install && npm run build
php artisan storage:link
```

If SSH is not available, you can skip this step as dependencies are already included.

4) Point the web root
- Ensure your domain points to the project’s `public/` directory.

5) Run the web installer
- Visit your domain (or `https://your-domain.com/install`). Follow the wizard to complete:
  - Server checks
  - Database details (host, port, name, username, password)
  - Site details (title, description)
  - Admin user (name, email, password)

Notes:
- The installer writes a default `.env` automatically. You don’t need to create it.
- After completion, you’ll see “Installation Complete” and a button to open the admin panel.

---

## Method B: FileZilla (FTP/SFTP)

Use this when you deploy via FTP/SFTP from your machine.

1) Upload package
- Connect with FileZilla to your server (SFTP preferred).
- Navigate to the target directory (document root for the site).
- Upload the larpress ZIP.

2) Extract on server
- If your host has a control panel: extract the ZIP in File Manager.
- If you have SSH:

```bash
unzip larpress.zip -d .
```

3) Install dependencies (Optional)
- The package already includes `vendor/` and pre-built npm assets, so this step is **optional**.
- If you want to update dependencies or rebuild assets, run these from the project root (SSH required):

```bash
cd /path/to/your/site
composer install --no-dev --optimize-autoloader
npm install && npm run build
php artisan storage:link
```

4) Point the web root to `public/` and run the web installer at your domain.

What the installer configures
- Creates default `.env`
- Saves database configuration
- Generates app key
- Captures site title/description
- Creates the initial admin user

---

## Method C: Web Installer from Git/SSH (Recommended)

### Step 1: Download larpress

```bash
# Clone from GitHub
git clone https://github.com/Pacific-Softwares/larpress-demo.git
cd larpress

# Or download ZIP
wget https://github.com/Pacific-Softwares/larpress-demo/archive/main.zip
unzip main.zip
cd larpress-main
```

### Step 2: Install Dependencies

```bash
# Install PHP dependencies
composer install --no-dev

# Install Node dependencies
npm install
npm run build
```

### Step 3: Set Permissions

```bash
# Set proper permissions
chown -R www-data:www-data storage bootstrap/cache
```

### Step 4: Run Web Installer

```bash
# Start development server
php artisan serve

# Or configure your web server to point to /public
```

Visit `http://your-domain.com/install` in your browser.

### Step 5: Follow Installation Wizard

The web installer will guide you through:

1. **System Check** - Verifies server requirements
2. **Database Setup** - Configure database connection
3. **Admin Account** - Create first admin user
4. **Site Settings** - Set site name, URL, email
5. **Finalize** - Complete installation

::: tip
Keep your database credentials handy. You'll need:
- Database host
- Database name
- Database username
- Database password
:::

## Method 2: Manual Installation

### Step 1: Prepare Environment

```bash
# Clone repository
git clone https://github.com/Pacific-Softwares/larpress-demo.git
cd larpress

# Copy environment file
cp .env.example .env
```

### Step 2: Configure Environment

Edit `.env` file with your settings:

```env
APP_NAME=larpress
APP_ENV=production
APP_KEY=
APP_DEBUG=false
APP_URL=https://your-domain.com

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=larpress
DB_USERNAME=root
DB_PASSWORD=your_password

CACHE_DRIVER=file
QUEUE_CONNECTION=database
SESSION_DRIVER=database
```

### Step 3: Install Dependencies

```bash
# Install Composer dependencies
composer install --optimize-autoloader --no-dev

# Install NPM dependencies
npm install
npm run build
```

### Step 4: Generate Application Key

```bash
php artisan key:generate
```

### Step 5: Run Migrations

```bash
php artisan migrate --seed
```

### Step 6: Create Storage Link

```bash
php artisan storage:link
```


## Next Steps

After installation:

1. [Configure your application](/getting-started/configuration)
2. [Explore the admin panel](/admin-panel/overview)
3. [Create your first module](/modules/creating)
4. [Install a theme](/themes/introduction)

## Getting Help

If you encounter issues:

- Check [Common Issues](/troubleshooting)
- Join [Discord Community](https://discord.gg/larpress)
- Create [GitHub Issue](https://github.com/Pacific-Softwares/larpress/issues)

