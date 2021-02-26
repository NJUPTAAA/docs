# Test Cases

!> If you want further information, see: [NJUPTAAA/rsync](https://github.com/NJUPTAAA/rsync);

1. NOJ uses `rsync` to sync test cases between main service and judge server. You don't have to install `rsync` manually, we have a docker image available for you.
    - [Docker](https://www.docker.com/)
    - [Docker-Compose](https://docs.docker.com/compose/)

2. Access Main Service Server as `root`, then run the following;

```bash
docker pull njuptaaa/rsync
```

Then run the following command to get an exmaple for `docker-compose.yml`:

```bash
git clone https://github.com/NJUPTAAA/rsync
cd rsync
cp docker-compose.mainservice.example.yml docker-compose.yml
vim docker-compose.yml
```

The edit `docker-compose.yml` and the file should look just like:

```yml
version: "3"
services:
  noj-rsync-master:
    image: njuptaaa/rsync
    container_name: noj-rsync
    volumes:
      - $PWD/storage/test_case:/test_case
      - $PWD/storage/logs:/log
    environment:
      - RSYNC_MODE=master
      - RSYNC_USER=ojrsync
      - RSYNC_PASSWORD=CHANGE_THIS_PASSWORD
    ports:
      - "0.0.0.0:873:873"
```

Then type `docker-compose up -d` and make master rsync service running.

!> Remember to let port `873` open and change the field `RSYNC_PASSWORD`.


3. Now Access Judge Server as `root`, then run the following;

```bash
docker pull njuptaaa/rsync
```

Then run the following command to get an exmaple for `docker-compose.yml`:

```bash
git clone https://github.com/NJUPTAAA/rsync
cd rsync
cp docker-compose.judgeserver.example.yml docker-compose.yml
vim docker-compose.yml
```

The edit `docker-compose.yml` and the file should look just like:

```yml
version: "3"
services:
  noj-rsync-slave:
    image: njuptaaa/rsync
    container_name: noj-rsync
    volumes:
      - $PWD/data/backend/test_case:/test_case
      - $PWD/data/rsync_log:/log
    environment:
      - RSYNC_MODE=slave
      - RSYNC_USER=ojrsync
      - RSYNC_PASSWORD=CHANGE_THIS_PASSWORD
      - RSYNC_MASTER_ADDR=NOJ_MAIN_SERVICE_ADDR
```

Then type `docker-compose up -d` and make salve rsync service running.

!> Remember to change the field `RSYNC_PASSWORD` and fill your main service address to `RSYNC_MASTER_ADDR`, it should look like `192.168.0.2` or `acm.njupt.edu.cn`.

4. All done!