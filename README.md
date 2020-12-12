# heap_dump
dump heap memory of running process

Use [`gdb`](https://www.gnu.org/software/gdb/) to dump the *heap* memory of running process.  
Run as **root**!

```console
#!/bin/bash
$PROG=${1:vim}   # vim as default
for PID in `ps -C $PROG -o pid= | tr -d ' '`
do 
  gdb --pid $PID -ex "dump memory dump_$PID `grep heap /proc/$PID/maps | awk '{ print $1 }' | sed -E 's/([^\-]+?)-([^\-]+?)/0x\1 0x\2/'`" --batch
done
```
