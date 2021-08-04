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
This would start a monitor process that will process all time consuming jobs and handle those jobs. Note that once the `queue:work` command has started, it will continue to run until it is manually stopped or you close your terminal. So this is only for test environment.

Jobs in `high` queue has the most priority and `low` has the least priority, normally, NOJ puts all jobs in `normal` queue.

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

## Babel Judge Sync

NOJ Babel needs remtoe verdict synchronization for virtual judges. Those doesn't require queue but works similar to queues.

### Basic

To start NOJ Babel Judge Sync, simply typing this command:
```bash
php artisan babel:judge
```
This would start a process that will process and handle all virtual-judge submissions. Note that once the `babel:judge` command has started, it will continue to run until it is manually stopped or you close your terminal. So this is only for test environment.

### Daemon

NOJ recommend using Supervisor for Daemon porcess.

1. Supervisor configuration files are typically stored in the `/etc/supervisor/conf.d` directory. Within this directory, you may create any number of configuration files that instruct supervisor how your processes should be monitored. We need to create a `.conf` file that starts and monitors a `babel:judge` process:

```ini
[program:NOJJudgeSync]
process_name=%(program_name)s_%(process_num)02d
command=php /path-to-noj/artisan babel:judge
autostart=true
autorestart=true
user=www
numprocs=1
```

The `numprocs` directive will instruct Supervisor to run 1 `babel:judge` processe and monitor it, automatically restarting it if fail.

!> `numprocs` should always be 1, unlike above sections which you can set any number you wish.

2. Once the configuration file has been created, you may update the Supervisor configuration and start the processes using the following commands:

```bash
sudo supervisorctl reread

sudo supervisorctl update

sudo supervisorctl start NOJJudgeSync:*
```

3. For more information on Supervisor, consult the [Supervisor documentation](http://supervisord.org/index.html).
