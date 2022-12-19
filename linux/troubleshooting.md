- [Network](network)
- [SSH](#ssh)
- [Miscellaneous](miscellaneous)


# Network

# Network manager does not start
For network manager a fix I made is the following in the */etc/fstab* file you can remove all references to _netdev and it should improve some things. In the log you gave me, I don't see any error concerning gnome or gdm itself, you should see the xorg logs to see if it runs. Already made a test by removing the references to _netdev which can echo some problems.

==> Replace "compress=zstd,_netdev" with "compress=zstd" 

# SSH

## sign_and_send_pubkey: no mutual signature supported

```bash
ssh -p 22 -i ~/.ssh/key.dsa user@route.th2.prod
```

To get around this, I had to modify the config of my SSH client to accept the use of DSA keys: 

```bash
sudo vim /etc/ssh/ssh_config
PubkeyAcceptedKeyTypes +ssh-dss
```

# Miscellaneous

## command-not-found 

```bash
Désolé, command-not-found s'est arrêté anormalement ! Veuillez remplir un rapport de bogue à : 
https://bugs.launchpad.net/command-not-found/+filebug
Veuillez inclure les informations suivantes dans le rapport :
Version de command-not-found : 0.3
Version de python : 3.8.10 final 0 
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.3 LTS
Release:    20.04
Codename:   focal
Information sur l'exception : 
unable to open database file
Traceback (most recent call last):
 File "/usr/lib/python3/dist-packages/CommandNotFound/util.py", line 23, in crash_guard
   callback()
 File "/usr/lib/command-not-found", line 90, in main
   cnf = CommandNotFound.CommandNotFound(options.data_dir)
 File "/usr/lib/python3/dist-packages/CommandNotFound/CommandNotFound.py", line 79, in __init__
   self.db = SqliteDatabase(dbpath)
 File "/usr/lib/python3/dist-packages/CommandNotFound/db/db.py", line 12, in __init__
   self.con = sqlite3.connect(filename)
sqlite3.OperationalError: unable to open database file

Fix:
chmod ugo+r /var/lib/command-not-found/commands.db
chmod 2755 /var/lib/command-not-found/
```
