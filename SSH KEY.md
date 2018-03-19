# SSH Key's
Als erstes wurde auf die Maschine verbunden, ins .ssh verzeichnis gewechselt und der Key rausgeholt.
```ruby
vagrant@dhcp:~$ cd .ssh
vagrant@dhcp:~/.ssh$ ls
authorized_keys
vagrant@dhcp:~/.ssh$ cat authorized_keys
```
Nach dem cat erhält man diesen Key:
## DHCP Maschine 
```
# CLOUD_IMG: This file was created/modified by the Cloud Image build process
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3ZWeT/56Z4sOdWTbM3pTA3f3YLgvTXVzatbkvx8ydyKGPU2rv51zJRqtixoJPYusVRs+tJH9WyBuUm57xd9bdncUxVxyyqQINTHnUUhUf...
```
Nachdem man diesen Key gefunden hat, braucht man noch einen auf dem lokalen Gerät. Dafür muss man zuerst in den Ordner wechseln, indem das .ssh File liegt.
In meinem Fall war das im C/users/arranai/.ssh.
Falls es dort noch keine Key hat, gibt man ```ssh-keygen``` ein und erstellt somit ganz einfach einen Key.
## Lokal 
```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA0iNzObFmf9+PcptuhufTGOzek0LBlhgXSXbUxuaxe0CUznWp
...
-----END RSA PRIVATE KEY-----
```
