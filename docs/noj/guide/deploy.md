# Deploy

1. You need to have a server with Nginx or Apache installed and installed the following:
    - [PHP 7.3(Recommend 7.3.6)](http://php.net/downloads.php)
    - [Composer](https://getcomposer.org)
    - [MySQL 5.7(Recommend 8.0)](https://www.mysql.com/)
    - [Redis 3.2.1(Recommend 5.0)](https://redis.io)

!> Notice: If you are a green hand and are using `Linux`, we recommend you `lnmp`, it's an open-source script for installing `Nginx`, `Mysql` and `PHP`. It can also be used install `Redis` as well. Check https://lnmp.org for more info.

2. Clone NOJ to your website folder;

```bash
cd /path-to-noj/
git clone https://github.com/ZsgsDesign/NOJ ./
```

3. Change your website root to `public` folder and then, if there is a `open_basedir` restriction, remove it;

4. Now run the following commands at the root folder of NOJ;

```bash
composer install
```

!> Notice: you may find this step(or others) fails with message like "func() has been disabled for security reasons", it means you need to remove restrictions on those functions, basically Laravel and Composer require `proc_open()`, `popen()` and `proc_get_status()` to work properly.

5. Almost done, you still got to modify a few folders and give them permission to write;

```bash
cd /path-to-noj/
chown -R www:www ./
```

NOJ need all directories to 755 and all files to 644, it should be done by default, if you are having concerns, try the following:

```bash
sudo find /path-to-noj/ -type f -exec chmod 644 {} \;
sudo find /path-to-noj/ -type d -exec chmod 755 {} \;
```

!> Notice: In former docs we advised users to chage `storage/` and `bootstrap/` to `775` recursively, but now that approach is highly discouraged due to security concerns. We recommend the above approach much better. `www` is the default Nginx user name, for `Apache` it would be `www-data`, Notice that in your server that user might be slightly differect.

6. OK, right now we still need to configure environment, a typical `.env` just like the `.env.example`, you simply need to type the following codes;

```bash
cp .env.example .env
vim .env
```

After editing `.env`, use this to generate a new key:

```bash
php artisan key:generate
```

7. Now, we need to configure the database, thankfully Laravel has migration already;

```bash
php artisan migrate
```

!> Notice: Make sure you have `.env` configured already, or this may lead to unpredictable bugs.


8. Since `0.4.1` NOJ uses `Passport` for API Auth Services, you need to install it first;

```bash
php artisan passport:install
```

9. At last, we need to configure scheduling system for NOJ;

```bash
crontab -e
* * * * * php /path-to-noj/artisan schedule:run
```

!> Notice: NOJ Task Schedule runs lots of tasks, like sync judger or refresh ranks, you can check anytime at **NOJ Admin Panel**.

10. NOJ's Website can now be accessed by public, enjoy!

