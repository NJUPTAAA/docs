# Basic Upgrade

1. Turn your application into Maintenance Mode.

```bash
php artisan down
```

2. Pull new codes from our git source.

```bash
git pull
```

3. Install composer packages.

```bash
composer install
```

4. Migrate Database.

```bash
php artisan migrate
```

5. Notice that since `NOJ 0.5.0` we introduced `Laravel 6.x`, that may break some of your compiled views. So it is adviced to **always** run the following code to clear the view in case of further changes.

```bash
php artisan view:clear
```

6. Notice that since `NOJ 0.16.0` we introduced `NPM` and `TypeScript`, so it is required to install node.js packages each time you upgrade NOJ since `0.16.0`.

```bash
npm install
```

7. Notice that since `NOJ 0.16.0` we introduced `Webpack`, So it it required to compile and pack static resources each time you upgrade NOJ since `0.16.0`.

```bash
npm run production
```

8. Make your application live again.

```bash
php artisan up
```

!> If you use supervisor for queue, you shall run `supervisorctl reload` after each upgrate, see [Configure Queue](noj/guide/queue.md) for more details.