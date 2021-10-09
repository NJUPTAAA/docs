# Upgrade to 0.17.0 Characinae

NOJ 0.17.0 Characinae brings structure changes to NOJ, which requires extra attention.

!> Note that since this version NOJ introduces brand new PDF generation method, please install it first.

1. When upgrade to 0.17.0, you need to **run step 1 to 7 from [Basic Upgrade](noj/upgrade/basic.md) frist**. We also updated Basic Upgrade, you may found the process a bit harder.

2. Now, after step 7, we need to configure some new environment variables.

`FUNC_STRONG_PASSWORD` controlls whether only account with strong passwords can registered, defaults to `false`:

```ini
FUNC_STRONG_PASSWORD=false
```

`PAGINATION_PROBLEM_PER_PAGE` controlls how much problem are shown each page, defaults to `20`:

```ini
PAGINATION_PROBLEM_PER_PAGE=20
```

!> Note that if maintainers set this value too high, it may cause some performance issues. Recommend values are between 10 and 50.

`WKHTML_PDF_BINARY` and `WKHTML_IMG_BINARY` denotes the executable path of wkhtmltopdf:

```ini
WKHTML_PDF_BINARY="/usr/local/bin/wkhtmltopdf"
WKHTML_IMG_BINARY="/usr/local/bin/wkhtmltoimage"
```

3. Update the BABEL Extension NOJ that bundles with each version release, you can do that via command:

```bash
php artisan babel:install noj
```

!> Note that it is not `babel:update`, that command applies to extension that managed by BABEL registry, BABEL Extension NOJ comes with each version of NOJ thus not managed by BABEL registry.

4. Now make your application live again.

```bash
php artisan up
```

!> Note that if you use supervisor for queue, you shall run `supervisorctl reload` after each upgrade, see [Configure Queue](noj/guide/queue.md) for more details.