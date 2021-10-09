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

5. Notice that since `NOJ 0.5.0` we introduced `Laravel 6.x` and later in `NOJ 0.17.0` we introduced `Laravel 8.5`, that may break some of your compiled views. So it is adviced to **always** run the following code to clear the view in case of further changes.

```bash
php artisan view:clear
```

6. Notice that since `NOJ 0.16.0` we introduced `NPM` and `TypeScript`, so it is required to install node.js packages each time you upgrade NOJ since `0.16.0`.

```bash
npm ci
```

!> Note that `npm install` would update packages from `package.json`, it's different from `composer install` and thus **NEVER** use it in NOJ.

7. Notice that since `NOJ 0.16.0` we introduced `Webpack`, so it is required to compile and bundle static resources each time you upgrade NOJ since `0.16.0`.

```bash
npm run production
```

8. Update the BABEL Extension NOJ that bundles with each version release, you can do that via command:

```bash
php artisan babel:install noj
```

!> Note that it is not `babel:update`, that command applies to extension that managed by BABEL registry, BABEL Extension NOJ comes with each version of NOJ thus not managed by BABEL registry.

9. Make your application live again.

```bash
php artisan up
```

!> If you use supervisor for queue, you shall run `supervisorctl reload` after each upgrate, see [Configure Queue](noj/guide/queue.md) for more details.