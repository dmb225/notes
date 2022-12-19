- [SCP](scp)
- [Authentication](authentication)



# Authentication

[How to use SSH keys for authentication](https://upcloud.com/resources/tutorials/use-ssh-keys-authentication)

[To accept SSH connections whose server is not present in the "known hosts" list](https://linuxhint.com/ssh-stricthostkeychecking/)

## ~/.ssh/config

[OpenSSH Config File Examples For Linux / Unix Users](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/)

## Still getting password prompt

[Why am I still getting a password prompt with ssh with public key authentication?](https://unix.stackexchange.com/questions/36540/why-am-i-still-getting-a-password-prompt-with-ssh-with-public-key-authentication)


# SCP

```bash
scp -i ~/.ssh/lbs.dsa lbs@build-route-datacook-001.mappy.priv:/mnt/data/fpm_2006_44/pbf/idf.osm.pbf data/fpm_2006_44/pbf/ 
scp build-route-data-001:routemm-doc.zip routemm-doc1.zip
scp /home/jenkins/.ssh/* jenkins@build-route-slave-001:/home/jenkins/.ssh 
```

# SSH Tunnel

[Port forwarding](https://github.com/phidra/notes/blob/main/structured/ssh/port_forwarding.md)

```bash
ssh -i ~/.ssh/monitor.dsa -N -L 5672:localhost:5672 monitor@recette-route-engine-001.th2.prod 
ssh -N -L 8000:recette-route-engine-002.th2.prod:8000 recette-route-engine-002 
```
