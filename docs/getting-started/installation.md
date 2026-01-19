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

### Step 1: Upload Package

1. Download the larpress release ZIP.
2. In your panel, open File Manager and navigate to your target directory:
   - Root domain: `public_html/`
   - Subdomain/addon: that site's document root
3. Upload the ZIP to the target directory.

![Upload ZIP to cPanel](/src/cpanel-zip-upload.png)

### Step 2: Extract Files

Use "Extract" in File Manager to unzip the archive into the target directory.

![Extract ZIP in cPanel](/src/cpanel-zip-extract.png)

### Step 3: Move Files to public_html

If you extracted the ZIP in a subdirectory, move all files to the `public_html/` directory (or your site's document root).

![Move Files to public_html](/src/cpanel-move-to-public_html.png)

### Step 4: Create Database

Before running the installer, create a MySQL database and user:

1. **Create Database:**
   - Go to MySQL Databases in cPanel
   - Create a new database (e.g., `larpress_db`)

![Create Database in cPanel](/src/cpanel-databse-create.png)

2. **Create Database User:**
   - Create a new MySQL user (e.g., `larpress_user`)
   - Set a strong password

![Create Database User in cPanel](/src/cpanel-databse-usere-create.png)

3. **Assign Permissions:**
   - Add the user to the database
   - Grant ALL PRIVILEGES to the user

![Assign Database Permissions](/src/cpanel-db-user-permissions.png)

::: tip
Keep your database credentials (database name, username, password) handy. You'll need them during the installation wizard.
:::

### Step 5: Install Dependencies (Optional)

The package already includes `vendor/` and pre-built npm assets, so this step is **optional**.
- If you want to update dependencies or rebuild assets, run these from the project root (SSH required):

```bash
composer install --no-dev --optimize-autoloader
npm install && npm run build
php artisan storage:link
```

If SSH is not available, you can skip this step as dependencies are already included.

### Step 6: Point the Web Root

Ensure your domain points to the project's `public/` directory.

### Nginx Configuration

If you're using **Nginx** as your web server, you need to make two important changes to your Nginx configuration:

**Change 1: Set the root directive to the public directory**

```nginx
root <PATH_TO_YOUR_PROJECT_DIR>/public;
```

**Change 2: Use `$realpath_root` instead of `$document_root` in fastcgi_param**

```nginx
fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
```

**Complete Nginx server block example:**

```nginx
server {
    listen 80;
    server_name your-domain.com;
    root <PATH_TO_YOUR_PROJECT_DIR>/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

::: tip
Replace `<PATH_TO_YOUR_PROJECT_DIR>` with the actual path to your project directory. For example: `/var/www/larpress` or `/home/user/larpress`.
:::

After making these changes, reload Nginx:

```bash
sudo nginx -t  # Test configuration
sudo systemctl reload nginx  # Reload Nginx
```

### Step 7: Run the Web Installer

Visit your domain (or `https://your-domain.com/install`). The web installer will guide you through the installation process.

#### Installation Step 1: Welcome

The installer starts with a welcome screen and system requirements check.

![Installation Step 1](/src/installation-step-1.png)

#### Installation Step 2: Database Configuration

Enter your database credentials:
- Database host (usually `localhost` or `127.0.0.1`)
- Database port (usually `3306`)
- Database name
- Database username
- Database password

![Installation Step 2](/src/installation-step-2.png)

#### Installation Step 3: Site Information

Configure your site details:
- Site name
- Site URL
- Site description

![Installation Step 3](/src/installation-step-3.png)

#### Installation Step 4: Admin Account

Create your first admin user:
- Admin name
- Admin email
- Admin password

![Installation Step 4](/src/installation-step-4.png)

#### Installation Step 5: Finalize

Review your settings and complete the installation.

![Installation Step 5](/src/installation-step-5.png)

#### Installation Success

Once installation is complete, you'll see a success message with options to:
- Go to Admin Panel
- Visit Homepage

![Installation Success](/src/installation-success.png)

![Installation Success - Homepage](/src/installation-success-home.png)

![Installation Success - Login](/src/installation-success-login.png)

::: tip
The installer writes a default `.env` automatically. You don't need to create it manually.
:::

Notes:
- The installer automatically creates the `.env` file with your configuration
- After completion, you can access the admin panel at `/admin/login`
- Your admin credentials are the ones you set during installation

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
git clone https://github.com/yourusername/larpress.git
cd larpress

# Or download ZIP
wget https://github.com/yourusername/larpress/archive/main.zip
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

The web installer will guide you through the installation process with visual steps:

1. **Welcome & System Check** - Verifies server requirements
   ![Installation Step 1](/src/installation-step-1.png)

2. **Database Setup** - Configure database connection
   ![Installation Step 2](/src/installation-step-2.png)

3. **Site Settings** - Set site name, URL, description
   ![Installation Step 3](/src/installation-step-3.png)

4. **Admin Account** - Create first admin user
   ![Installation Step 4](/src/installation-step-4.png)

5. **Finalize** - Review and complete installation
   ![Installation Step 5](/src/installation-step-5.png)

6. **Success** - Installation complete!
   ![Installation Success](/src/installation-success.png)

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
git clone https://github.com/yourusername/larpress.git
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
2. [Create your first module](/modules/creating)
3. [Install a theme](/modules/system/themes)

## Getting Help

If you encounter issues:

- Join [Discord Community](https://discord.gg/larpress)
- Create [GitHub Issue](https://github.com/yourusername/larpress/issues)

