# เทคนิคต่าง ๆ ที่ใช้ในคลิป
1. การ pull image จาก docker
2. การแสดง images ที่มีในเครื่อง
3. การ run mysql container
4. การทำ data persistence ด้วย volume เพื่อเก็บข้อมูลของฐานข้อมูลไว้

## mysql on docker hub : [mysql](https://hub.docker.com/_/mysql)
---


### script สำคัญที่ใช้ในคลิปนี้
```
$ docker --version
```

### pull docker image
```
$ docker pull mysql
```

### list images
```
$ docker images
```

### run mysql on docker
```
$ docker run --name dolphin --rm -p 3306:3306 -e MYSQL_ROOT_PASSWORD=banana -d mysql:latest
```
* ``--name`` ตั้งชื่อให้ Container
* ``--rm`` สั่งให้ลบ Container เมื่อมีการหยุดทำงาน
* ``-p`` คำสั่งกำหนด Port
* `` 3306:3306`` ท่อนแรกกำหนด Port ให้ฝั่ง Host ท่อนที่สองกำหนด Port ให้ฝั่ง Container
* `` 3306:3306`` ท่อนแรกกำหนด Port ให้ฝั่ง Host ท่อนที่สองกำหนด Port ให้ฝั่ง Container
* ``-e`` ย่อมาจาก Envalopement valiable ที่เราจะบอก
* ``MYSQL_ROOT_PASSWORD=banana`` ตั้ง Password ว่า banana
* ``-d`` คือ การ Run แบบ demon คือการ Run พวก Service หมายความว่าจะรับบริการจากผู้ใช้
* ``mysql:latest`` ชื่อของ Image และ Tag
*  เมื่อ Run ผ่านจะได้ Containaer ID : ` 86a7e6611960d8bd82f80202ea1af7bab8664e31fc1fa5f232da5361450dba03`


### list processes
```
$ docker ps -a
```

### exec command in container
```
$ docker exec -it dolphin bash
$ docker exec -it dolphin mysql -u root -p
```
* `-it` Interactive terminal

    ```
    root@86a7e6611960:/#
    ```
    
* `# cat /etc/os-release` -> ตรวจสอบ Linux Version
    ```
    root@86a7e6611960:/# cat /etc/os-release
    ``` 

* ` # which mysql` -> มี mysql อยู่ไหม
    ```
    root@86a7e6611960:/# which mysql
    ```

* `# mysql -u root -p` -> Run mysql
    ```
    root@86a7e6611960:/# mysql -u root -p
    Enter password:
    ```
    * show database
        ```
        mysql> show databases;
        ```
    * create database
        ```
        mysql> create database drink;
        ```
    * use database
        ```
        mysql> use drink;
        ```
    * create table
        ```
        mysql> create table menu(id int, descr varchar(50), price int);
        ```
    * show tables
        ```
        mysql> show tables;
        ```
    * insert menu
        ```
        mysql> insert into menu values (1, 'coffee', 40), (2, 'tea', 30);
        ```
    * quit
        ```
        mysql> \q
        ```



    

### connect to mysql from terminal
```
# mysql -u root -p -h localhost -P 3306 --protocol=tcp
# mysql -u root -p -P 3306 --protocol=tcp
# mysqlsh root@localhost:3306 --sql
```

### stop process
```
docker stop dolphin
```

## persist data (using volume)
```
docker run --name dolphin --rm -p 3306:3306 -d -e MYSQL_ROOT_PASSWORD=banana -v mysqlvolume:/var/lib/mysql mysql
```


<!-- 10:15/23:59 -->


```
$ git init
$ git add .
$ git commit -m "first commit"
$ git branch -M main
$ git remote add origin https://github.com/YuttanaSRMUTT/BasicDocker.git
$ git push -u origin main
```

### git tag
```
$ git add .
$ git commit -m "v1.0"
$ git tag v1.0
$ git push origin v1.0
$ git push -d origin v1.0
```