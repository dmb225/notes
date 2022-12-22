[Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html)

- [Archives](#archives)
- [Boot](#boot)
- [Disk](#disk)
- [DNS](#dns)
- [Files](files)
- [History](#history)
- [Memory](#memory)
- [Networking](#networking)
- [Postgres](#postgres)
- [Processes](#processes)
- [Search](#search)
- [Server](#server)
- [SSH](#ssh)

# Archives

```bash
tar -zxvf /livraison/v0.0/data/toto.tgz -C ./home/dir
```

# Boot

[Reboot Linux System Command](https://www.cyberciti.biz/faq/howto-reboot-linux/)

## service

```bash
sudo service snapd restart
```

# Disk

[10 Commands to Check Disk Partitions and Disk Space on Linux](https://www.binarytides.com/linux-command-check-disk-partitions/)

```bash
du -sh .

du -hs *
```

# DNS

## dig

```bash
dig +short gitlab.toto.priv @10.0.1.200
```

## mcli

```bash
nmcli connection show MyVPN | grep dns
```

# Files

## ln

```bash
ln -fs "${dir1}" "${9dir2}"

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

## ls

```bash
ls -L bin
```

## md5sum

```bash
md5sum "${output_path}/${france}.osm.pbf" |awk '{print $1}' > "${output_path}/${france}.osm.pbf.md5"
```

## tail

```bash
tailf routemm | grep "92.*400.*GET" | grep APIX

tail -f --lines=10000 /var/log/tornik/tornik-traffic|grep "traffic situations in
```

## tee

```bash
<command> 2>&1 # redirects stderr into stdout 
<command> | tee <file> # redirects standard output to both the console and a file
<command> 2>&1 | tee <file> # both previous
<command> >/dev/null 2>&1 # Hide standard and error outputs
```

# History

```bash
echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_aliases
```

# Memory

```bash
free -m
```

# Networking

## nc

```bash
nc -zv <address> <port> -w <timeout>
```

## netstat
```bash
netstat -a -n | grep 5672 
```

## tcpdump

```bash
l
```

## telnet

```bash
telnet <address> <port>
```

# Postgres

```bash
dpkg -l |grep -e postgres -e postgis
```


# Processes

## ps

```bash
ps aux|grep redis-server|grep -v grep

ps aux|grep redis-server|grep -v grep|awk '{print $2}'
```

## kill

```bash
kill -9 $(ps -elf | grep <name> | awk '{print $4}')

pkill -f "\.\/<name>"

kill_<some_processes> () {
    arr=$(ps -ef | grep <name> | awk '{print $2}')
    for i in $arr; do kill -9 $i; done;
}
```

# Search

[Find with a regex path](https://www.linuxquestions.org/questions/)

## find
```bash
find -L <directory_path> -name *<file_name>*

find -L . -name *LTE*

find /route/data/closed_sections/ -type d | sort -n | tail -n 1 | cut -d '/' -f5  # last create directory

find / -type d | grep <directory_name>

find ./ -regextype posix-egrep -regex ".*/(dir1|dir2)/.*"
```

## grep

[Find files having specific text](https://stackoverflow.com/questions/16956810/how-to-find-all-files-containing-specific-text-string-on-linux)

```bash
grep -rnw '/path/to/somewhere/' -e 'pattern'

grep -R -o 'ITIMM-[0-9]*' | cut -d ':' -f2 > itimm.txt
```

# Server

## curl

```bash
curl snap-route-mm-001.mappy.priv/ 2>/dev/null | jq -r '.manifest.commit' 

curl localhost:8007/st_pedestrian_route_rpc -d@<file.json>

curl --location --request GET 'https://toto.net/myapi/7.0/routes?from=2.581988,48.880588&to=2.2491160684509803,48.81781779236697&clientid=titi&lang=fr_FR&departure=true&qid=idSameRequest&providers=tc' --header 'apikey: xIfzQzDcpozke'

time curl -XGET -I -H "referer: https://fr.toto.com/" -H "apikey: f2wjQp1eFdTe26Y" https://api.toto.net/myapi/7.0/routes\?from\=2.350849%2C48.856895\&to\=1.476738%2C49.398658\&lang\=fr_FR\&providers\=car

time curl -XGET -I https://toto.net/myapi/7.0/routes\?from\=2.350849%2C48.856895\&to\=1.476738%2C49.398658\&lang\=fr_FR\&providers\=car
```
