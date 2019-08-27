# Judging Queue

# Basic

To start NOJ Judging Queue, simply typing this command:
```bash
php artisan queue:work --queue=noj
```
This would start a monitor process that will process all user submissions and handle those submissions to judge servers or remote judge. How ever once stopped this process the process would be on halt. So this is only for test environment.

If you have multiple Babel Extensions, just add then to the queue, like:
```bash
php artisan queue:work --queue=noj,codeforces,contesthunter,poj,vijos,pta,uva,hdu,uvalive
```

# Daemon

