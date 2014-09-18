Tools
=====

Online Schema Change
--------------------
Change table-schemas without locking the table with [Percona's](http://www.percona.com/) pt-online-schema-change

**Usage**

```shell
pt-online-schema-change --execute --critical-load="Threads_running:500" --max-load "Threads_running:250" --charset=utf8 --user=root --ask-pass --database=[database] t=[table] --alter='ADD `userId` int(10) unsigned NOT NULL DEFAULT '0', ADD `createStamp` int(10) unsigned NOT NULL DEFAULT '0', ADD KEY `createStamp` (`createStamp`), ADD KEY `userId` (`userId`)'
```

**Download**

[Percona Toolkit for MySQL](http://www.percona.com/software/percona-toolkit)

**Full Documentation**

http://www.percona.com/doc/percona-toolkit/2.2/pt-online-schema-change.html

**IMPORTANT**

Read the full [documentation](http://www.percona.com/doc/percona-toolkit/2.2/pt-online-schema-change.html) before using it, there a lot of peculiarities that need to be considered before using this tool.


SSH
---
**Create key**

```bash
ssh-keygen -t rsa -f ~/.ssh/id_rsa -P ''
```

**Copy public key to remote machine**

```bash
ssh-copy-id root@<REMOTE_HOST>
```

**Initiate port forwarding**

```bash
ssh -NL *:8086:<REMOTE_HOST>:8086 root@<REMOTE_HOST>
```

**Forward remote port to local**

```bash
ssh -NR *:1234:localhost:80 root@<REMOTE_HOST>
```
(`GatewayPorts yes` in `sshd_config` required to bind to non-loopback interface)


Git
---
**Deleting branch on github**

```bash
git push origin --delete <branchName>
```


OpenSSL
-------
If you omit `-out` output defaults to STDOUT

**Convert PFX to key+pem**

```
openssl pkcs12 -in <PFX file> -nocerts -nodes -out <KEY File>
openssl pkcs12 -in <PFX File> -clcerts -nokeys -out <PEM File>
```

**Create key+csr**

```
openssl req -new -newkey rsa:2048 -nodes -keyout <KEY File> -out <CSR File> -subj '/CN=<DOMAIN | WILDCARD>/C=<COUNTRY>'
```

**Create key+pem with sha-256 signature (aka self-signed certificate)**
`sha-1` signed certificates are being [gradually phased out in a near future](http://www.entrust.com/sha-1-deprecation-on-to-sha-2/)
```
openssl req -x509 -nodes -sha256 -days 3650 -newkey rsa:2048 -keyout <KEY File> -out <PEM File> '/CN=<DOMAIN | WILDCARD>/C=<COUNTRY>'
```

**Output hash of certificate (used by apache for chain following)**
```
openssl x509 -noout -hash -in <PEM File>
```

**Create new csr based on existing certificate**
```
openssl x509 -x509toreq -in <PEM File> -signkey <KEY file> -out <CSR file>
```

ffmpeg
------
**Convert `MTS` to `mp4`**
```
cp /Volumes/NO\ NAME/PRIVATE/AVCHD/BDMV/STREAM/* .
rm -rf /Volumes/NO\ NAME/PRIVATE/AVCHD
ffmpeg -i concat:"00001.MTS|00004.MTS|00005.MTS" -vcodec copy -acodec copy result.mp4
```

rdiff-backup
------------
**Restoring database backup**
This script gives only the big picture, it's not suitable to be run without modifying it.
```sh
HOST="<IP ADDRESS OF DATABASE SERVER>"

echo "Restoring latest backup..."
rm -rf /tmp/restore-db
rdiff-backup --restore-as-of now /home/backup/db /tmp/restore-db

echo "Copying to $HOST..."
scp -pr -C -o CompressionLevel=9 /tmp/restore-db root@$HOST:/var/lib/mysql
rm -rf /tmp/restore-db
```

PhpStorm
--------
Version 8 required.

**Vagrant PhpStorm Tunnel**

To run scripts using PHP (installed in the Vagrant virtual machine) via ssh, install
[vagrant-phpstorm-tunnel](https://github.com/cargomedia/vagrant-phpstorm-tunnel) and follow the instructions to set it up.

**PHPUnit Test Configuration**

Go to `Preferences > PHP > PHPUnit` and under `PHPUnit library` specify composer's `autoload.php` as custom loader. Under `Test runner` check the checkbox next to `Default configuration file` and select the `phpunit.xml` inside the root folder of the project you're setting up.
![PhpStorm screenshot](img/phpstorm-phpunit-configuration.png)
