rdiff-backup
============
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
