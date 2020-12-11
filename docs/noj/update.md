# Update NOJ

1. Turn your application into Maintenance Mode.

```bash
php artisan down
```

2. Pull new codes from our git source.

```bash
git pull
```

3. Install new packages.

```bash
composer install
```

4. Migrate Database.

```bash
php artisan migrate
```

5. Notice that since `NOJ 0.5.0` we introduced `Laravel 7.x`, that may break some of your compiled views. So it is adviced to **always** run the following code to clear the view in case of further changes.

```bash
php artisan view:clear
```

5. Make your application live again.

```bash
php artisan up
```

!> If you use supervisor for queue, you shall run `supervisorctl reload` after each update, see [Configure Queue](noj/guide/queue.md) for more details.