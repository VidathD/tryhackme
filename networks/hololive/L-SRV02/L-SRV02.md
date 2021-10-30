# L-SRV02 Docker Container

We entered this docker container by exploiting RCE in [L-SRV01](../L-SRV01/L-SRV01.md) web server.

## Enumeration

Using netcat to portscan with `nc -zv 192.168.100.100 1-65535`