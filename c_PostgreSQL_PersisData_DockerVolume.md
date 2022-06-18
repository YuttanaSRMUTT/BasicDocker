## PortgreSQL
### 1. Pull PortgreSQL image
```
$ docker pull postgres
```
### 2. ตรวจสอบ image ของ PortgreSQL ที่ดึงมาได้
```
$ docker images
```
### 3. วิธีการ Run PortgreSQL
```
$ docker run --name pegasus --rm -e POSTGRES_PASSWORD=banana -d -p 5432:5432 postgres
```
<!-- creat -->
| Command | Description |
| --- | --- |
`--name` | ตั้งชื่อให้ image `--name pegasus`|
`--rm` | เมื่อมีการ Stop ระบบจะลบ container ออก |
`-e` | Environment Variables `-e POSTGRES_PASSWORD=banana`|
`-d` | มักใช้กับการ Run Database Server หรือกับ Server ต่างๆ |
`-p` | ระบุ Port ที่ใช้ Run `-p 5432:5432`|

### 4.เช็คว่า Run จริงแล้วหรือยัง
```
$ docker ps -a
$ docker exec -it pegasus psql -U postgres
```
```
postgres=# \l
postgres=# create database foody;`
postgres=# \c foody
postgres=# \d
foody=# create table menu(id int, decscr text, price int);
foody=# insert into menu values (1, 'rice', 15), (2, 'water', 8);
foody=# select * from menu;
foody=# \q
```

| Command |Description|
|---|---|
|`\l` | |
|`create database foody;` | |
|`\c foody` | |
|`create table menu(id int, decscr text, price int);` | |
|`insert into menu values (1, 'rice', 15), (2, 'water', 8);` | |



### 5. เช็คว่า เครื่องเรามี postgres ติดตั้งไว้แล้วหรือยัง
```
$ which psql
$ psql -U postgres -h localhost
postgres=# \q
``` 


### 6. การ Persist data [`Link postgres docker`](https://hub.docker.com/_/postgres)

```
$ docker run --name pegasus --rm -e POSTGRES_PASSWORD=banana -d -p 5432:5432 -v pgdatavolume:/var/lib/postgresql/data postgres
```

| Command |Description|
|---|---|
|`-v pgdatavolume:/var/lib/postgresql/data`|PGDATA|
|`/var/lib/postgresql/data`|ใน Posrtgres จะเก็บ data ไว้ตรงนี้|

```
$ psql -U postgres -h localhost
```
```
postgres=# \l
postgres=# create database bakery;
postgres=# \c bakery
```

```
bakery=# \l
bakery=# create table menu(id int, desr text, price int);
bakery=# insert into menu values (1, 'cheese cake',120), (2, 'mable cake', 95);
bakery=# select * from menu;
bakery=# \q
```

```
$ docker ps -a
$ docker stop pegasus
$ docker run --name pegasus --rm -e POSTGRES_PASSWORD=banana -d -p 5432:5432 -v pgdatavolume:/var/lib/postgresql/data postgres
```

```
postgres=# \l
postgres=# \c bakery
```

```
bakery=# \d
bakery=# select * from menu;
bakery=# insert into menu values (3, 'coconut cake', 70);
bakery=# \q
```

```
$ docker stop pegasus
$ docker run --name unicorn --rm -e POSTGRES_PASSWORD=banana -d -p 5432:5432 -v pgdatavolume:/var/lib/postgresql/data postgres
$ psql -U postgres -h localhost
```

```
postgres=# 
postgres=# \l
postgres=# \c bakery
```

```
bakery=# select * from menu;
bakery=# \q
```

```
$ docker ps -a
$ docker stop unicorn
```

## GIT
```
$ git add .
$ git commit -m "3rd"
$ git push
```















