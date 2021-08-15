# Upgrade to 0.5.0 Aphyocharacinae

NOJ 0.5.0 Aphyocharacinae brings structure changes to NOJ. Which requires extra attention.

!> Note that since this version NOJ requires Composer `^2.0` and PHP `^7.4`.

1. Before upgrade to 0.5.0, you need to upgrade your PHP to `7.4` or above, then run `composer self-update` if you are not using Composer 2.

!> If you are updating Composer from 1 to 2. you also need to remove `vendor` folder located in NOJ root folder.

1. When upgrade to 0.5.0, you need to **run commands from [Basic Upgrade](noj/upgrade/basic.md) frist**.

2. Now, before last step, which makes your application live again. Check Queue Configuration and configure the new **Babel Judge Sync Queue**, see [Configure Queue](noj/guide/queue.md) for more details.

```ini
[program:NOJJudgeSync]
process_name=%(program_name)s_%(process_num)02d
command=php /path-to-noj/artisan babel:judge
autostart=true
autorestart=true
user=www
numprocs=1
```

3. The new NOJ 0.5.0 also uses a new user permission system, so you need to run the following command:

```bash
php artisan manage:permission --action=grant --uid=1 --permission=1
```

It will give user `1` the **front admin permission**, which gives admin badge and a navbar link to Admin Portal.

!> Note that Admin Portal still requires **independent user password authentication**.

4. The new NOJ 0.5.0 also modifies socialite login logics, now you need to enable each socialite method **independently** using `GITHUB_ENABLE` and `AAUTH_ENABLE`.

Github config:
```ini
GITHUB_ENABLE=true
GITHUB_KEY=
GITHUB_SECRET=
GITHUB_CALLBACK_URL= # should be like http://www.your-noj-website.com/oauth/github/callback
```

AAuth Config:
```ini
AAUTH_ENABLE=true
AAUTH_KEY=
AAUTH_SECRET=
AAUTH_CALLBACK_URL= # should be like http://www.your-noj-website.com/oauth/aauth/callback
```

The Callback URL however, is configured **mostly on remote services**. You just need to configure the link in comment, for example: `https://acm.njupt.edu.cn/oauth/github/callback`.

5. The new NOJ 0.5.0 provides themes support, you can pick one from [Theme](noj/guide/theme.md) and configure it as follows:

```ini
APP_THEME=byzantium
```

6. The new NOJ 0.5.0 comes with two OAuth related switches as follow:

```ini
APP_ALLOW_OAUTH_TEMP_ACCOUNT=false
FUNC_ENABLE_REGISTER=true
```

`APP_ALLOW_OAUTH_TEMP_ACCOUNT` controls whether social account login users without binding NOJ account first can login or not. If enabled, NOJ would create a temp acoount with random email address and usernames, this account comes with no password and cannot logined via password/email until users create independent passwords.

`FUNC_ENABLE_REGISTER` controls whether users can register new accounts.

7. The new NOJ 0.5.0 provides fully new terms logic, admins can now create custom terms for NOJ sites in Admin Portal. If you want to use pre-built terms template, just fill in the blanks as follow:

```ini
TERM_SUBJECT_FULL_NAME="NJUPT Online Judge"
TERM_SUBJECT_NAME="NOJ"
TERM_STREET="9 Wenyuan Road"
TERM_CITY="Nanjing"
TERM_PROVINCE="Jiangsu"
TERM_STATE="China"
TERM_ZIP="221000"
TERM_CONTACT_EMAIL="noj@njupt.edu.cn"
```

8. The new NOJ 0.5.0 also requires NOJ_JudgeServer **v0.2.1 or above**. please upgrate your NOJ_JudgeServer accordingly.

9. Now make your application live again.

```bash
php artisan up
```

!> Note that if you use supervisor for queue, you shall run `supervisorctl reload` after each upgrade, see [Configure Queue](noj/guide/queue.md) for more details.