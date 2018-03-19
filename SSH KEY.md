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
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC3ZWeT/56Z4sOdWTbM3pTA3f3YLgvTXVzatbkvx8ydyKGPU2rv51zJRqtixoJPYusVRs+tJH9WyBuUm57xd9bdncUxVxyyqQINTHnUUhUfa6KuPOSOrZZbMZZ1YxhX7nwilBn4yJjws/q7OUdEZ07SV739ZkQVq/55dDGr9nxcNEbUnojCqkJsCL0l8dPbzhSjDXXBaXcMhXovJJwgR0nTbhXQ8J1uYxnV6k97dkdnRl1LBnRQaDz0o/K42EjFUaSKhTskV9AVzh6gZxz8Z87au2kuS17VEE216Ur1OG3iodYesnLlwLmSTjaIX9YFZrAaFevVrFNJJYnv4//jbv9F vagrant
vagrant@dhcp:~/.ssh$ exit
```
Nachdem man diesen Key gefunden hat, braucht man noch einen auf dem lokalen Gerät. Dafür muss man zuerst in den Ordner wechseln, indem das .ssh File liegt.
In meinem Fall war das im C/users/arranai/.ssh.
Falls es dort noch keine Key hat, gibt man ```ssh-keygen``` ein und erstellt somit ganz einfach einen Key.
## Lokal 
```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA0iNzObFmf9+PcptuhufTGOzek0LBlhgXSXbUxuaxe0CUznWp
oMI8GxNsf2RXEafdZjNdOk0Wv6OQZe/ntiZdmmuHOaysePmVm7WtcDvGZyuO7EQ+
jMHgfXiTaywja7UJeFacZU3F8SHppNe3On/FpkO4Rbdpl/K03p9HvIKgO3I69pzd
SW6m30ot4QJutTEeWEc5sM1CGdaw2u3EYtHalN1jb2TQ5NffOz2tqpMw7kGGY7qv
cyRxLfuMOI2tZXRrYdiXenH+1z/cqUUX9WHqcYofX7Fetj/kD7WWsrB2XC+qAz/w
lcwNpQfzapYy/Pl5aAOI+KsJ3AXn/ho1yeB0sQIDAQABAoIBACaUW5M7/pV7ddqU
rrYV2au50SM4HlJwGdZi+q2JrQvzz14YPAxHnMFbz4+T3GhhaURaKcOKY6LLZLdS
VDgc0xKGq0zrZr7PE6iCslTopIRMevDllpZBAfYHLQmAEQC1PAfb3tq6bJzYnQym
jf0veBoOVMZ35er/pDU7CPCTCtfey6j/GcXk3cRvf+qsw9g5/EF/vM5GvXhpK4SI
GFTwENo6195er99fZzIUoXj2mkF6xWeT/oXRKhSmsICw42hpKtaPP9C68CQlqpDW
Lste7ugjg/W4kRiSccYQ9nr9Zai/DCToQEDDzbMSjI5gqrlQxIBeZK7L+37Pvm11
wN2+wAECgYEA9RxI+pl5u07gYFxSSJhJmVrqLcuvRD+785piExPgzsFFnMGH9/k9
RhpGHD7y6Q89+zy7CsAULg5tzGxp26/gZaBKOhk6KlDHscfnQQBE1eYrAemisqyi
6oWhfjSTkV7zTZyK5DZaBAOv7lJHEwZvNp8jN/axrMv2YD4b73luqbkCgYEA23lq
+brhGPu0mpQT7NCx+jExghCdvd66p9que5WSSOJSoAPZ0icxm3rtnr+KFagZLy/9
eJNpHY1+qSwcPhtwNWvlCaKxAMzQXXcjS1mWZLwAOCiDoiQXTs4a+kfnF+wdRzXu
z5XTxb1A4P15fAGHlXvg48p4drSWZcRUcBy1PrkCgYEA0pUfefW7qRomGYOXyfjU
WqXKRdgV10vufWbo1b0hSmCwHvICkCAY7Y6LJ59JcMQAm0Xc6GqHq94HpTaLaAvd
fVJOE0YzO8G1H19Apg7GFQMvdfA1MM6zFUwDp/shwSZTYB2bEmBDy+kjEFyt5YGE
sOfeCSmwEmYVYTBbLc4lLjkCgYByHaO9zamU7+tsJGpny+t+h22Sj0k1nEW5WT84
CwFQ3DzR7q6nUrG8giJjVHxb3leZ7X4B38PcFeIx3DmjIWkqnbstU2ZtYBFHR9cW
KrLEFeyXRpmLCPEFjK0CTbie+6oNiMFvNhwyyMCfO6ybCcCRvSOlzXTtY+B/caHl
2Ud0IQKBgCTW4UmdJUV5bUk1qn3bV8qxAb/uXVa7zew9WQ277bcmntIsAdYi0Rln
15yeGW+qU+eWWFO7F/pPdgMUZXTc9QViO912ZoMu8NhzYgutQdoaOG9uFjyJBh5Q
BCo/CAYC2JE5nNpoFv4kHew+f8mPNd3cPFruRcqchg4+834CnHVp
-----END RSA PRIVATE KEY-----
```
