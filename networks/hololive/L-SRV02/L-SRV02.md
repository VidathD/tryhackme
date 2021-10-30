# L-SRV02 Docker Container

We entered this docker container by exploiting RCE in [L-SRV01](../L-SRV01/L-SRV01.md) web server.

## Enumeration

Using netcat to portscan with `nc -zv 127.0.0.1 1-65535` we find that following ports are open.

```
localhost [127.0.0.1] 3306 (mysql) open
localhost [127.0.0.1] 80 (http) open
```

