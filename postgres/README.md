# postgres

## db

Start latest postgres image in Docker with local data volume:

```shell
docker run \
    --name postgres \
    -e POSTGRES_USER=test \
    -e POSTGRES_PASSWORD=test \
    -p 5432:5432 \
    -v ${PWD}/data:/var/lib/postgresql/data \
    -d postgres
```

## client 

In separate terminal:

> on mac, if you don't have `psql` installed, you can `brew install libpq`, just make sure to add `/opt/homebrew/opt/libpq/bin` to your path after (follow brew instructions after the install)

```shell
psql -h localhost -U test
```

Enter the above defined password `test`, and you should see the `psql` prompt: 

```shell
psql (15.2)
Type "help" for help.
test=#
```

## query 

From here on, you can run queries against that database and all the data will be persisted in the `./data` directory. 

```shell
\l
```

## schema 

To create a schema using local file:

```shell
psql -h localhost -Utest < ./schema.sql
```

## export

```shell
pg_dump -h localhost -Utest -d test -t books --column-inserts --data-only > ./books.sql
```

## import 

```shell
pg_dump -h localhost -Utest -d test -t books < ./books.sql
```