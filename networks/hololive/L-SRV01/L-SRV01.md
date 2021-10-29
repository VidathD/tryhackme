# L-SRV01 Webserver

## Reconnaissance

### Ports

### Webserver: vhosts

### Webserver: Fuzz

### Webserver: robots.txt


## Exploit

We found an interesting file in `admin.holo.live/robots.txt` called `/var/www/admin/supersecretdir/creds.txt`. This gave a `403` status code when trying to read.

### LFI in dev.holo.live/img

`dev.holo.live` takes the parameter `file`. This is vulnerable to LFI.

Payload: `curl http://dev.holo.live/img.php?file=../../../../var/www/admin/supersecretdir/creds.txt`

Exploit: [[exploit](exploit/LFI/exploit.sh)]

Loot: