# Deploy NOJ with Docker [experimental]

1. You need to have a server with Docker Installed.

2. Create `docker-compose.yml`:

```yml
version: '2'

services:
  db:
    image: 'docker.io/bitnami/mysql:8.0'
    environment:
      - MYSQL_ROOT_PASSWORD=my_password
      - MYSQL_USER=my_user
      - MYSQL_DATABASE=my_database
      - MYSQL_PASSWORD=my_password
      - MYSQL_AUTHENTICATION_PLUGIN=mysql_native_password
    volumes:
      - 'mysql_data:/bitnami/mysql/data'

  redis:
    image: 'docker.io/bitnami/redis:6.0'
    environment:
      # ALLOW_EMPTY_PASSWORD is recommended only for development.
      - ALLOW_EMPTY_PASSWORD=yes
      - REDIS_DISABLE_COMMANDS=FLUSHDB,FLUSHALL
    ports:
      - '6379:6379'
    volumes:
      - 'redis_data:/bitnami/redis/data'

  noj:
    tty: true
    image: 'docker.io/bitnami/laravel:7'
    environment:
      - DB_HOST=db
      - DB_USERNAME=my_user
      - DB_DATABASE=my_database
      - DB_PASSWORD=my_password
      - CACHE_DRIVER=redis
      - REDIS_HOST=redis
      - REDIS_PASSWORD=null
      - LOG_CHANNEL=stderr
      # WARNING: change the key below, generate a new one using
      # docker-compose exec myapp php artisan key:generate --show
      - APP_KEY=base64:jp/GeCEFvqpbEUJQ/OkOSm+u8lYFDRB0HXBy/uwbr34=
    depends_on:
      - db
      - redis
    ports:
      - 3000:3000
    volumes:
      - ./:/app
    # privileged: true # Privileged mode could be required to run this container under Windows

  judge_server:
      image: njuptaaa/judge_server
      restart: always
      read_only: true
      cap_drop:
          - SETPCAP
          - MKNOD
          - NET_BIND_SERVICE
          - SYS_CHROOT
          - SETFCAP
          - FSETID
      tmpfs:
          - /tmp
      volumes:
          - $PWD/tests/test_case:/test_case:ro
          - $PWD/log:/log
          # - $PWD/server:/code:ro
          - $PWD/run:/judger
      environment:
          - BACKEND_URL=http://noj:3000/api/judge_server_heartbeat
          - SERVICE_URL=http://judge-server:12358
          - TOKEN=base64:jp/GeCEFvqpbEUJQ/OkOSm+u8lYFDRB0HXBy/uwbr34=
      ports:
          - 12358:8080

volumes:
  redis_data:
    driver: local
  mysql_data:
    driver: local
```