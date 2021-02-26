# General Commands to Linux

##Create Alias
alias hh='history'

history -c -> limpa o diretório
nl -> shows the lines of file with your line number 
wc -l -> number of lines in a file
wc -w -> number of words in a file
wc -c -> number of bites in a file
wc -m -> number of caracteres in a file
sort -n -> makes the sort by number

last reboot -> Reboot history
route -n -> Routing table of Kernel
time traceroute -> time of processing
(x)cowsay, cmatrix

init 0
telinit 0
halt
seq 1 10
seq 1 10 >(>) filename.txt

sudo adduser username
su username
passwd username
lastlog
last
logname
id
cat /etc/passwd
userdel -r username

sudo addgroup $groupname
cat /etc/group
groups
adduser $username $groupname
gpasswd -a $groupname
gpasswd -d $username $groupname
groupdel $groupname

Permissions
r - read
w - write
x - execution
ls -lh
d - diretorio
- - file

drwxr-xr-x
x type => - or d
xxx owner => --- | -wx | r-x | rw- | --x | -w-
xxx group
xxx others

chmod 

gzip $filename
gzip -9 $filename
gunzip $filename.gz

zip $filename.zip $filenames
unzip $filename.zip

bzip2 $filename
bzip2 $filename.bz2

rar a $filename.rar $filenames
rar x $filename.rar 

tar -cf $filename.tar $filenames
tar -xvf $filename.tar.gz
tar -xvf $filename.tar.gz -C $dirname

sudo apt install $packageName
sudo apt upgrade $packageName
sudo apt remove $packageName
sudo apt update && sudo apt upgrade

sudo dpkg -i $packageName.deb
sudo dpkg -I $packageName.deb
sudo dpkg -r $packageName

sudo rpm -ivh $packageName.rpm
sudo rpm -ivh --nodeps $packageName.rpm
sudo rpm -U $packageName.rpm
sudo rpm -e $packageName.rpm

sudo yum install $packageName
sudo yum update $packageName
sudo yum remove $packageName

