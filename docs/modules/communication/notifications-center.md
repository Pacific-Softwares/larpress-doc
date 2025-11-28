# Notification Preferences

Control which notification channels you receive system notifications through. Each user can customize their notification preferences individually.

Access via **Admin Panel → Communication → Notification Preferences**.

## Overview

Notification Preferences allows you to choose how you receive different types of system notifications. You can enable or disable notifications for each channel (Email, SMS, Web Notification) independently for each notification type.

## Available Notification Types

The system automatically creates preferences for the following notification types:

1. **New Registration** - Notifications when new users register
2. **Welcome Email** - Welcome email notifications
3. **Forgot Password** - Notifications for password reset requests
4. **Reset Password Confirmation** - Confirmation notifications after password reset
5. **Contact Confirmation** - Confirmation when contact forms are submitted
6. **New Contact Enquiry** - Notifications for new contact form submissions

## Notification Channels

For each notification type, you can control three delivery channels:

### Email
- Receive notifications via email
- Requires email configuration in Settings → Email
- Notifications are sent to your registered email address

### SMS
- Receive notifications via SMS/text message
- Requires SMS configuration in Settings → SMS (Twilio)
- Notifications are sent to your registered phone number

### Web Notification
- Receive in-app notifications
- Appears as bell icon alerts in the admin panel
- No external service configuration required

## Using Notification Preferences

### Accessing Preferences

1. Navigate to **Admin Panel → Communication → Notification Preferences**
2. You'll see a table with all available notification types
3. Each row shows one notification type with three toggle switches

### Configuring Preferences

The interface displays a grid with 4 columns:
- **Notification Type** - The name of the notification
- **SMS** - Toggle to enable/disable SMS notifications
- **Email** - Toggle to enable/disable email notifications
- **Web Notification** - Toggle to enable/disable in-app notifications

### Saving Changes

1. Toggle the switches for each notification type and channel as desired
2. Click **Save** to apply your changes
3. A success notification confirms your preferences have been updated

## How It Works

### Auto-Creation

When you first access Notification Preferences, the system automatically creates preference records for all default notification types. If a preference doesn't exist, it will be created with all channels disabled by default.

### Per-User Settings

- Each user has their own notification preferences
- Preferences are stored per user ID and permission name
- Changes only affect your own notifications, not other users

### Database Storage

Preferences are stored in the `notification_preferences` table with the following structure:
- `user_id` - The user who owns the preference
- `permission_name` - The notification type identifier
- `email` - Boolean flag for email channel
- `sms` - Boolean flag for SMS channel
- `web_notification` - Boolean flag for web notification channel

## Best Practices

1. **Review Regularly** - Check your notification preferences periodically to ensure you're receiving important notifications
2. **Channel Selection** - Choose the most appropriate channel for each notification type:
   - Use **Email** for important notifications you want to archive
   - Use **SMS** for urgent notifications that need immediate attention
   - Use **Web Notification** for less critical notifications you can check in-app
3. **Avoid Overload** - Don't enable all channels for all notification types to avoid notification fatigue
4. **Test Configuration** - Ensure email and SMS services are properly configured in Settings before enabling those channels

## Integration with Notification System

When the application sends notifications, it checks your preferences:
- If a channel is enabled for a notification type, you'll receive the notification via that channel
- If all channels are disabled for a notification type, you won't receive that notification
- The system respects your preferences automatically

## Developer Notes

### Adding New Notification Types

To add new notification types:

1. Add the permission name to the `$defaults` array in `NotificationPreferences.php`
2. Add a display label to the `$labels` array
3. The system will automatically create preferences for all users on their next access

### Accessing Preferences in Code

```php
use App\Models\NotificationPreference;

// Check if user wants email notifications for a specific type
$pref = NotificationPreference::where('user_id', $userId)
    ->where('permission_name', 'new_registration')
    ->first();

if ($pref && $pref->email) {
    // Send email notification
}

// Check SMS preference
if ($pref && $pref->sms) {
    // Send SMS notification
}

// Check web notification preference
if ($pref && $pref->web_notification) {
    // Create in-app notification
}
```

## Tips

- Preferences are user-specific, so each team member can customize their own notifications
- Disabled channels won't send notifications even if the service is configured
- Web notifications appear in the admin panel's notification bell icon
- Email and SMS notifications require proper service configuration in Settings
- You can enable/disable channels independently - you don't need to enable all three
