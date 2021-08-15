# Artisan Commands

## Management Tools

### Randomize Password

```bash
# Reset user 1's password to a 9 digits random pass
php artisan manage:resetpass --uid=1 --digit=9
```

### Create Admin User

```bash
php artisan manage:create-admin
```

### Ban User

```bash
#The time parameter allows for all formats to strtotime function of php.
php artisan manage:ban --user=1 --reason="Violation of user instructions" --time="+365 days"
```

### Permission

Action can be `grant`,`revoke`,`list`.
UID is the id of the target user.
Permission is the id of a permission, check id via running `php artisan manage:permission` directly.

```bash
php artisan manage:permission --action=grant --uid=1 --permission=1
```

## Babel

See **Babel Section**.