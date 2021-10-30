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