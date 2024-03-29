# Upgrade to 0.16.0 Bryconinae

NOJ 0.16.0 Bryconinae brings structure changes to NOJ, which requires extra attention.

!> Note that since this version NOJ requires at least Chrome 69 or equivalent and requires `npm` package management from now on, you can install `npm` and `Node.js` from [Node.js Download Page](https://nodejs.org/en/download/).

1. When upgrade to 0.16.0, you need to **run step 1 to 5 from [Basic Upgrade](noj/upgrade/basic.md) frist**. We also updated Basic Upgrade, you may found the process a bit harder.

2. Now, after step 5, you may notice something new. Since 0.16.0 we introduced `NPM` and `TypeScript`, so it is required to install node.js packages each time you upgrade NOJ since `0.16.0`.

```bash
npm ci
```

!> Note that `npm install` would update packages from `package.json`, it's different from `composer install` and thus **NEVER** use it in NOJ.

3. Since `NOJ 0.16.0` we introduced `Webpack`, so it is required to compile and bundle static resources each time you upgrade NOJ since `0.16.0`.

```bash
npm run production
```

!> Note that it may display one warning, that is ok.

4. Now make your application live again.

```bash
php artisan up
```

!> Note that if you use supervisor for queue, you shall run `supervisorctl reload` after each upgrade, see [Configure Queue](noj/guide/queue.md) for more details.