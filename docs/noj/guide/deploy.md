# Deploy

1. You need to have a server with Nginx or Apache installed and installed the following:
    - [PHP 7.3(Recommend 7.3.6)](http://php.net/downloads.php)
    - [Composer](https://getcomposer.org)
    - [MySQL 5.7(Recommend 8.0)](https://www.mysql.com/)
    - [Redis 3.2.1(Recommend 5.0)](https://redis.io)

!> Notice: If you are a green hand and are using `Linux`, we recommend you `lnmp`, it's an open-source script for installing `Nginx`, `Mysql` and `PHP`. It can also be used install `Redis` as well. Check https://lnmp.org for more info.

2. Clone NOJ to your website folder;

```
cd /path-to-noj/
git clone https://github.com/ZsgsDesign/NOJ ./
```

3. Change your website root to `public` folder and then, if there is a `open_basedir` restriction, remove it;

4. Now run the following commands at the root folder of NOJ;

```
composer install
```

!> Notice: you may find this step(or others) fails with message like "func() has been disabled for security reasons", it means you need to remove restrictions on those functions, basically Laravel and Composer require `proc_open()`, `popen()` and `proc_get_status()` to work properly.

5. Almost done, you still got to modify a few folders and give them permission to write;

```
chmod -R 775 storage/
chmod -R 775 bootstrap/
```

6. OK, right now we still need to configure environment, a typical `.env` just like the `.env.example`, you simply need to type the following codes;

```
cp .env.example .env
vim .env
```

After editing `.env`, use this to generate a new key:

```
php artisan key:generate
```

7. Now, we need to configure the database, thankfully Laravel has migration already;

```
php artisan migrate
```

!> Notice: Make sure you have `.env` configured already, or this may lead to unpredictable bugs.


8. At last, we need to configure scheduling system for NOJ;

```
crontab -e
* * * * * php /path-to-noj/artisan schedule:run
```

!> Notice: NOJ Task Schedule runs lots of tasks, like sync judger or refresh ranks, you can check anytime at **NOJ Admin Panel**.

9. NOJ's Website can now be accessed by public, enjoy!