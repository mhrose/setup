# My linux notes

## Navigate
* [File Search](#file-search)
* [Command Handlers](#command-handlers)
* [Web and Network](#web-and-network)
* [Git related](#git-related)
* [Arch in virtualbox](#arch-in-virtualbox)
	- [Mount shared drive](#mount-shared-drive)

***

## Clean Arch

```bash
pacman -Scc
pacman -Qtdq
sudo pacman -Rns $(pacman -Qtdq)
sudo du -sh ~/.cache/
rm -rf ~/.cache/*
```

## Little tricks

Update zsh
```bash
upgrade_oh_my_zsh
```

screen shoot (based on imagemagic)
```bash
import ~/test.png
```

resize based on imagemagic to new size %
```bash
convert -resize 70% source.png dest.jpg
```

Clear bash history (remember all terminals otherwise re-created from cache)
```bash
history -c
```

list python versions
```bash
ls /usr/bin/python*
```

Disk Utilization (-sh for human readable and then folder..)
```bash
lsblk
df -h
du -sh /*
```

***
## File Search

If search for specific file e.g.

```bash
sudo find / -name virtualenvwrapper.sh
```

Search in all files in given dir
```bash
grep
```
-r recursive
-n line number
-w match whole word (exclude for all matches eg. -e '.py')
for reular expression use egrep
```bash
grep -rnw ./ -e 'sublime'
```
print specific line-range from file e.g. line 224 + 2 lines
```bash
sed -n '224,+2p' filepath
```
e.g find numbers with egrep (regrex) - cpr finder in comments
```bash
egrep -rn ./ -e '#.*[0-9]{10,10}'
```

e.g. find text and return filename (the 'l' option, to start from /)
```bash
grep -rl 'text to find' /
```

***
## Command Handlers

xargs

```bash
ls | xargs -I{} echo {}
```

or more usefull combined with git

```bash
ls | xargs -I{} git -C {} pull
```

Repeat command with watch
*example watch cpu temp each 3rd second*

```bash
watch -n 3 sensors | gerp xxx
```

***
## Network and Web

curl
wget
hey

### DNS lookup and more (Arch)

```bash
drill @nameserver
```

### the ip command

```
ip address
ip route (to find router see default)
```

***
## Arch in Virtualbox

Mount shared drive

*first make share in vbox gui*

```bash
sudo mount -t vboxsf VM-Share ~/vmshare

```

Add extra drive

```bash
fdisk -l

fdisk /dev/sdb

'n'
... xx default
'w' (for write!)
```

Format new disk

```bash
mkfs.ext4 /dev/sdb1
```

Add mountpoint

```bash
lsblk
mkdir -p mhrose
mount /dev/sdb1 ~/mhrose
lsblk
```

***
## Screen (also in oracle virtualbox for full screen)

See options and devices
```bash
xrandr
```

Set resolution eg. for external screen VGA1

```bash
xrandr --output VGA-1 --mode 1680x1050
```

***

## Listing and Creating Aliases

bash shell - add to .zshrc (or .bashrc)

`
alias [name="value"]
`

e.g.

```bash
alias boxcon="~/.dropbox-dist/dropboxd"
```
or

```bash
alias fixdisp="xrandr --output VGA-1 --mode 1680x1050"
```

***

## chmod

There are four OCTAL (0…7) digits, which control the file permissions.
But often, only three are used.
If you use 600 it equals 0600.
The missing digit is appended at the beginning of the number.
Each of three digits described permissions.
Position in the number defines to which group permissions do apply!

Permissions:
1 – can execute
2 – can write
4 – can read

The octal number is the sum of those free permissions, i.e.
3 (1+2) – can execute and write
6 (2+4) – can write and read

Position of the digit in value:
1 – what owner can
2 – what users in the file group(class) can
3 – what users not in the file group(class) can

Examples:
chmod 600 file – owner can read and write
chmod 700 file – owner can read, write and execute
chmod 666 file – all can read and write
chmod 777 file – all can read, write and execute

e.g. for git error when key is moved
WARNING: UNPROTECTED PRIVATE KEY FILE!
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

1
2
sudo chmod 600 ~/.ssh/id_rsa
sudo chmod 600 ~/.ssh/id_rsa.pub

## #### Install PKGBUILD

E.g use wget or clone from git...
In the dir containing the PKGBUILD (makepgk is part of pacman) run

```
makepkg
```

To install all dependancies (avaliable to pacman)

```bash
makepkg --syncdeps
```

In case of gcp issues and AUR files ... maybe go with

```bash
makepkg --skippgpcheck
```

Install newly build package with

```bash
sudo pacman -U /path-to-package.pkg.tar.xz
```


## ### ad to PATH

```
PATH=$PATH:~/opt/bin
PATH=~/opt/bin:$PATH
```

depending on whether you want to add ~/opt/bin at the end or at the beginning of the $PATH search

## /etc/host

/etc/hosts has the maximum priority, meaning this file is preferred ahead of any other name system

its primary present-day use is to bypass DNS


## Secure copy scp
Syntax:
scp (pretty close to the native cp)

from remote to local -r for recursively
scp -r devm:~/dummy-data/event-log.csv ./


scp ~/mhrose_git/toolbox/dev_vm/* mhrose@52.169.164.106:~/dev_vm

## To create a new symlink (will fail if symlink exists already):
ln -s /path/to/file /path/to/symlink
To create or update a symlink:
ln -sf /path/to/file /path/to/symlink


## systemctl
systemctl enable will hook the specified unit into relevant
places, so that it will automatically start on boot, or when relevant hardware is plugged in, or other situations depending on what's specified in the unit file.
systemctl disable are the opposite
Start a unit immediately:
systemctl start unit
Stop a unit immediately:
systemctl stop unit


## to list users:
cat /etc/passwd
To add a new user you can use:
sudo adduser new_username
To remove/delete a user, first you can use:
sudo userdel username
Then you may want to delete the home directory for the deleted user account :
sudo rm -r /home/username
To modify the username of a user:
usermod -l new_username old_username
To change the password for a user:
sudo passwd username
To change the shell for a user:
sudo chsh username

## Install from bootable USB
NOTE: wait with blank terminal for quite some time…. + 40 min…
wget https://downloads.sourceforge.net/manjarolinux/manjaro-xfce-17.0.2-stable-x86_64.iso
diskutil
diskutil list
sudo dd bs=1m of=/dev/rdisk2 if=manjaro-xfce-17.0.2-stable-x86_64.iso
The “r” device is the raw one. It will let you write 1 byte at a time. The other device is the block device for normal io.
dd is a command-line utility for Unix and Unix-like operating systems whose primary purpose is to convert and copy files.
In order to overwrite all the information on the disk, you have to make sure the mac OS isn’t using it first
Open the DiskUtility.app, and on your USB hard drive, unmount any of it’s partitions. Do not eject the USB hard drive.
Right click on the hard drive in the DiskUtility and get it’s Identifier from the Information tab.
Now take your image, and the identifier, and put it all together with something like this, on the command line in terminal:
dd if= of=/dev/


Extracting .tar.gz files

1) If your tar file is compressed using a gzip compressor, use this command to uncompress it.

    $ tar xvzf file.tar.gz

Where,

x: This option tells tar to extract the files.

v: The “v” stands for “verbose.” This option will list all of the files one by one in the archive.

z: The z option is very important and tells the tar command to uncompress the file (gzip).

f: This options tells tar that you are going to give it a file name to work with