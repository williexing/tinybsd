System:
FreeBSD  8.2-RELEASE

how to:

> updating /usr/src

#pkg\_add -rv cvsup-without-gui && rehash

#cvsup -g -L2 /usr/share/examples/cvsup/stable-supfile -h cvsup3.br.freebsd.org

> Check the directory /usr/src/tools/tools/tinybsd

#ls -la /usr/src/tools/tools/tinybsd/
total 32
drwxr-xr-x   3 root  wheel    512 Oct  7 12:32 .
drwxr-xr-x  61 root  wheel   1536 Oct  7 12:32 ..
-rw-r--r--   1 root  wheel   1478 Aug  3  2009 CHANGES
-rw-r--r--   1 root  wheel   9586 Aug  3  2009 README
drwxr-xr-x   9 root  wheel    512 Oct  7 12:32 conf
-rwxr-xr-x   1 root  wheel  13201 Oct 25  2010 tinybsd

> Inside _conf_ we have some pre-configured 'flavors'

# ls /usr/src/tools/tools/tinybsd/conf/
bridge		firewall	vpn		wrap
default		minimal		wireless

We choose default directory:

ls -la /usr/src/tools/tools/tinybsd/conf/default/
total 16
drwxr-xr-x  3 root  wheel   512 Oct  7 12:32 .
drwxr-xr-x  9 root  wheel   512 Oct  7 12:32 ..
-rw-r--r--  1 root  wheel  2971 Oct 10 07:05 TINYBSD
drwxr-xr-x  2 root  wheel   512 Oct  7 12:32 etc
-rw-r--r--  1 root  wheel  3926 Aug  3  2009 tinybsd.basefiles
-rw-r--r--  1 root  wheel   435 Aug  3  2009 tinybsd.ports

> Inside the TINYBSD file, we have the kernel configuration. Remove ADAPTATIVE\_GIANT and another stuff that you don't need. Insert the options:

options         COMPAT\_FREEBSD4         # Compatible with FreeBSD4
options         COMPAT\_FREEBSD5
options         COMPAT\_FREEBSD6
options         COMPAT\_FREEBSD7
options         CPU\_GEODE

:wq

> Inside etc directory, we have:

# ls etc/
fstab	rc.conf

> Now is time to create your image:
#cd /usr/src/tools/tools/tinybsd && ./tinybsd

> The script will do some questions about disk layout, use fdisk or diskinfo to get then.

> After some time, you can write the image using a live cd and dd tool. To make changes inside the image, mount as memorydisk using:

#cd /usr/src/tools/tools/tinybsd

#mdconfig -a -t vnode -f tinybsd.bin -u 0

#mount /dev/md0a /media



gg!