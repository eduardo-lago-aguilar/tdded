# Docker Compose Databases
Let's compose `development` and `test` database via `docker-compose` to allow both to exist locally at the same time, create a `docker-compose.yml` archive:

```yml
version: '3.2'

services:
  music_hive_development_db:
    image: postgres:9.5-alpine
    restart: always
    environment:
      POSTGRES_DB: music_hive_development
    ports:
      - 5432:5432

  music_hive_test_db:
    image: postgres:9.5-alpine
    restart: always
    environment:
      POSTGRES_DB: music_hive_test
    ports:
      - 5433:5432
```

launch the composition:

```bash
docker-compose up
```

edit `config/database.yml` and append `port` entry to `test` config:

```yml
test:
  #...
  port: 5433
```

check connection by issuing the specs:

```bash
rspec
```
