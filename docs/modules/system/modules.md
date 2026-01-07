# Modules Introduction

Modules are self-contained Laravel packages that extend larpress functionality. They allow you to add features without modifying core code.

## What are Modules?

Modules in larpress are:

- **Self-Contained** - Everything needed in one package
- **Installable** - Easy installation via ZIP or directory
- **Reusable** - Use across multiple projects
- **Maintainable** - Separate from core code
- **Shareable** - Distribute to others

## Module Structure

A typical module structure:

```
modules/{moduleSlug}/
├── Config/
│   └── config.php
├── Database/
│   ├── Migrations/
│   └── Seeders/
├── Http/
│   ├── Controllers/
│   ├── Middleware/
│   └── Requests/
├── Filament/
├── Models/
├── Providers/
│   └── {moduleSlug}ModuleRegisterServiceProvider.php
├── Resources/
│   ├── views/
├── Routes/
│   ├── web.php
│   ├── api.php
│   └── admin.php
├── assets/
│   ├── js/
│   └── css/
├── Installer.json
├── README.md
└── module.json
```

## Installing Modules

### Via Admin Panel - Marketplace

Access the module marketplace via **System → Modules → Add Module** to browse and install modules from the API marketplace.

![Add Modules](/src/add-modules.png)

**Features:**
- **Browse Modules** - View featured, popular, recommended, and favorite modules
- **Search & Filter** - Search by name, description, author, or tags. Filter by category
- **Install Modules** - One-click installation directly from the marketplace
- **Update Modules** - Automatic update detection and one-click updates
- **Activate/Deactivate** - Manage module activation status
- **Uninstall** - Remove modules (must be deactivated first)
- **Favorites** - Save modules to your favorites list
- **Reviews** - View and submit reviews for modules (premium members can review premium modules)
- **Support** - Get support for installed modules (premium members get support for premium modules)
- **Module Details** - View detailed information, screenshots, and reviews

**Installation Process:**
1. Browse modules in the marketplace
2. Click **Install** on your desired module
3. The module is automatically downloaded and installed
4. Click **Activate** to enable the module

**Membership Types:**
- **Free Users** - Can install and use free modules only
- **Premium Users** - Can install and use both free and premium modules
- Premium users can also review premium modules and get support for them

### Via Admin Panel - Manual Upload

1. Navigate to **System** → **Modules** in the admin panel.
2. Click **Upload Module** and select your module ZIP file.
3. After upload, the module will appear in the list—click **Activate** (or **Enable**) to turn it on.
4. During activation the installer will register service providers, run migrations, publish assets, and execute any tasks you defined in `Installer.json`.

### Use the Starter (Recommended)

1. Navigate to **System** → **Modules** in the admin panel.
2. Click **Download Sample Module**. This downloads a ZIP containing the scaffolded module.
3. Extract the ZIP locally to inspect the starter structure.
4. Rename the extracted folder to match your module slug (lowercase letters, numbers, hyphen, underscore). This slug should stay consistent with the `slug` you define in `module.json`.
5. Open the `module.json` manifest at the module root and update the metadata: `name`, `slug`, `version`, `description`, `author`, and any other values your module needs.
   - Keep the slug slugged using `/^[a-z0-9\-_]+$/` so the installer and CLI tooling can resolve it.
6. Customize the module:
   - Add controllers, routes, views, jobs, listeners, commands, config, migrations, and seeders.
   - Update `Providers/*ServiceProvider.php` to register bindings, hooks, and assets.
   - Modify `Installer.json` to script automated tasks like publishing assets, copying stubs, or seeding configuration.
7. When you are ready, re-compress the module directory into a ZIP file.
8. Return to **System** → **Modules**, click **Upload Module**, select your ZIP, and confirm.
9. After upload, the module will appear in the list—click **Activate** (or **Enable**) to turn it on.
10. During activation the installer will register service providers, run migrations, publish assets, and execute any tasks you defined in `Installer.json`.


### Module Configuration (`module.json`)

Each module has a `module.json` file:

```json
{
    "name": "Demo Module",
    "slug": "demo",
    "version": "1.0.0",
    "description": "A comprehensive demo module with categories, tags, and SEO features",
    "author": "Your Name",
    "email": "your@email.com",
    "homepage": "https://yourwebsite.com",
    "dependencies": {
        "php": ">=8.1",
        "laravel/framework": ">=10.0"
    },
    "settings": {
        "posts_per_page": 10,
        "enable_comments": true,
        "enable_categories": true,
        "enable_tags": true
    }
}
```

Required fields: `name`, `slug`, `version`. The `slug` must match `/^[a-z0-9\-_]+$/` and should match your folder name. Optional fields include `description`, `author`, `keywords`, `order`, `files`, `requires`, and `providers`. Use these to describe dependencies, wiring, and autoload behaviour for your module.



## Notes on iterative development and testing

- Every time you change module code locally, create a new ZIP of the module folder and upload it to update the module in the portal. Uploading a ZIP whose slug matches an existing module replaces it (unless that module is marked `protected`).

- For rapid iteration, modify files directly inside `modules/{ModuleName}/`. Example workflow:

  1. Suppose you uploaded a module with slug `demo`.
  2. Tweak controllers, routes, views, or resources under `modules/demo/*` to test immediately.
  3. Once satisfied, copy those updates back into your source module folder, re-zip, and upload again to keep the distributed package in sync.

**Important:** Runtime modules load from `modules/{ModuleName}/`. Keep a version-controlled source copy so your installer ZIP matches production.


Notes:

- Uploading a ZIP with the same module `slug` updates it in place (with backup, cache clear, and asset republish).


## Managing Modules

### Module Settings

Active modules can have configurable settings. Access module settings via **System → Modules → [Module Name] → Settings**.

**How it works:**
- Settings are automatically generated from the module's config file (`Config/{moduleSlug}.php`)
- Form fields are created based on config values (text inputs, toggles, selects, etc.)
- Helper text is extracted from config file comments
- Settings are saved directly to the config file
- Config cache is automatically cleared after saving

**Supported Field Types:**
- **Boolean values** → Toggle switches
- **Numeric values** → Number inputs
- **Arrays** → Tags input or Select (multi-select) for predefined options
- **Strings** → Text inputs
- **Key-value pairs** → Key-value field

**Special Handling:**
- Fields marked as "read-only" in config comments are excluded
- Comments above config keys are used as helper text
- Options can be defined in comments for dropdown fields

### Module Usage Instructions

Modules can provide usage instructions that are displayed in the admin panel. Instructions can be provided in two ways:

1. **USAGE.md File** - Create a `USAGE.md` file in the module root directory
2. **Service Provider Method** - Add a `getUsageInstructions()` method to your module's service provider

The instructions are displayed when viewing a module in the admin panel, helping users understand how to use the module.

## Module Development

Leverage the starter structure as a baseline, extending it with controllers, routes, models, Filament resources, and service providers. Keep business logic encapsulated within the module so it remains portable across projects.

## How Upload & Install Work (Under the Hood)

When you upload a module ZIP, larpress follows these steps:

1. Validate the uploaded file and extract it into a temporary directory.
2. Locate the module manifest (`module.json`) and optional `Installer.json` at the root or first nested directory.
3. Validate the required metadata (`name`, `slug`, `version`) and ensure the slug matches the expected pattern.
4. If a module with the same slug already exists:
   - Abort installation if the module is marked `protected`, keeping the current copy intact.
   - Otherwise back up the existing module, replace its files, republish assets, and clear caches.
5. For brand-new modules, copy the extracted files into `modules/{StudlyModuleName}/` and register them with the module registry.
6. Execute installer tasks:
   - Register service providers, routes, console commands, menus, permissions, and hooks exposed by the module.
   - Run migrations and seeders discovered inside the module or declared in `Installer.json`.
   - Publish assets to `public/modules/{slug}` or other targeted paths.
   - Run any additional installer commands defined in `Installer.json` (copy stubs, sync config, schedule jobs, etc.).
7. Update the module status so it can be enabled/disabled via the admin panel or CLI (`module:enable`, `module:disable`).
