# L-SRV01 Webserver

## Reconnaissance

### Ports

### Webserver: vhosts

### Webserver: Fuzz

### Webserver: robots.txt


## Exploit

We found an interesting file in `admin.holo.live/robots.txt` called `/var/www/admin/supersecretdir/creds.txt`. This gave a `403` status code when trying to read.

### LFI in dev.holo.live/img.php

`dev.holo.live/img.php` takes the parameter `file`. This is vulnerable to LFI.

Payload: `curl http://dev.holo.live/img.php?file=../../../../var/www/admin/supersecretdir/creds.txt`

Exploit: [exploit](exploit/LFI/exploit.sh)

Loot: [creds](exploit/LFI/creds.txt)

### RCE in admin.holo.live/dashboard.php

`admin.holo.live/dashboard.php` takes the parameter `cmd` which is passed through to host. This is vulnerable to RCE.

We can log into `admin.holo.live` using the creds we found using LFI above. 

Username: admin  
Password: DBManagerLogin!

Then we can execute system commands using `admin.holo.live/dashboard.php?cmd=COMMAND`.

We can get a reverse shell and from it. Looking around, we find that we are in the [L-SRV02](../L-SRV02/L-SRV02.md) docker container.

We got RCE via [L-SRV02](../L-SRV02/L-SRV02.md).

Now we can use linpeas to enumerate.