# Configure Queue

## Judging Queue

### Basic

To start NOJ Judging Queue, simply typing this command:
```bash
php artisan queue:work --queue=noj
```
This would start a monitor process that will process all user submissions and handle those submissions to judge servers or remote judge. Note that once the `queue:work` command has started, it will continue to run until it is manually stopped or you close your terminal. So this is only for test environment.

If you have multiple Babel Extensions, just add then to the queue, like:
```bash
php artisan queue:work --queue=noj,codeforces,contesthunter,poj,vijos,pta,uva,hdu,uvalive
```

### Daemon

NOJ recommend using Supervisor for Daemon porcess.

1. Supervisor configuration files are typically stored in the `/etc/supervisor/conf.d` directory. Within this directory, you may create any number of configuration files that instruct supervisor how your processes should be monitored. We need to create a `.conf` file that starts and monitors a `queue:work` process:

```ini
[program:NOJBabel]
process_name=%(program_name)s_%(process_num)02d
command=php /path-to-noj/artisan queue:work --queue=noj,codeforces,contesthunter,poj,vijos,pta,uva,hdu,uvalive
autostart=true
autorestart=true
user=www
numprocs=8
```

The `numprocs` directive will instruct Supervisor to run 8 `queue:work` processes and monitor all of them, automatically restarting them if they fail. You should change the `command` setion to meet your needs.

2. Once the configuration file has been created, you may update the Supervisor configuration and start the processes using the following commands:

```bash
sudo supervisorctl reread

sudo supervisorctl update

sudo supervisorctl start NOJBabel:*
```

3. For more information on Supervisor, consult the [Supervisor documentation](http://supervisord.org/index.html).

## Asynchronous Jobs

NOJ has some asynchronous jobs like **generate PDF** or **detect code plagiarism**. Those jobs also require queue.

### Basic

To start NOJ Asynchronous Jobs Queue, simply typing this command:
```bash
php artisan queue:work --queue=high,normal,low
```
This would start a monitor process that will process all user submissions and handle those submissions to judge servers or remote judge. Note that once the `queue:work` command has started, it will continue to run until it is manually stopped or you close your terminal. So this is only for test environment.

Jobs in `high` queue has the most priority and `low` has the least priority.

### Daemon

NOJ recommend using Supervisor for Daemon porcess.

1. Supervisor configuration files are typically stored in the `/etc/supervisor/conf.d` directory. Within this directory, you may create any number of configuration files that instruct supervisor how your processes should be monitored. We need to create a `.conf` file that starts and monitors a `queue:work` process:

```ini
[program:NOJ]
process_name=%(program_name)s_%(process_num)02d
command=php /path-to-noj/artisan queue:work --queue=high,normal,low
autostart=true
autorestart=true
user=www
numprocs=8
```

The `numprocs` directive will instruct Supervisor to run 8 `queue:work` processes and monitor all of them, automatically restarting them if they fail. You should change the `command` setion to meet your needs.

2. Once the configuration file has been created, you may update the Supervisor configuration and start the processes using the following commands:

```bash
sudo supervisorctl reread

sudo supervisorctl update

sudo supervisorctl start NOJ:*
```

3. For more information on Supervisor, consult the [Supervisor documentation](http://supervisord.org/index.html).
