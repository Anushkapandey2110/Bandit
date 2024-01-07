# Bandit
This repository contains writeup for helping in solving bandits
       BANDITS
               -Anushka Pandey


## Level 0
SSH command is used for remote login into a server 
It can login into different port numbers deployed on a server and it will act as a client to that server.
ssh bandit0@bandit.labs.overthewire.org -p 2220
 ls command - means list of available files
file <filename> - to see the type of file
cat <filename>-to read the content of the file

Password for Level 1 -
```
 NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```
## Level 1
The filename given is - 
Generally - represents an attribute so to specify that this is a filename we put ./ before -
Commands: 
 ssh bandit1@bandit.labs.overthewire.org -p 2220
ls 
cat  ./-
Password for level 2-
```
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
exit - for exiting from one server
## Level 2  
When there are spaces in a filename suppose the file has a name  “agatha books”
Now when we will use cat command to read the file the command will see agatha and books as different attributes to treat this as a single attribute we will use “agatha books “ or escape every space using backlash agatha\books
Commands used-
ls
cat  “filename with spaces”
Password for level 3 - 
```
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```
## Level 3 
The file is in a directory. 
To open a directory we use cd command.
Commands used-
cd <directoryname> this will change our directory from current to the directory given with cd command. 
Ls -a : to list all the files in the directory 
Password for Level 4-
```
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```
## Level 4
There are several files in the directory and the password is in one of the files
Commands used-
cd <directoryname>
ls -a
cat ./<filename> (the file names start with a dash)
Password for level 5 -
```
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```
## Level 5 
The file is in one of the multiple subdirectories of the directory inhere
It has a size of 1033 bytes , is human readable and is inexecutable
Commands used-
`ls -a`  It lists all the files hidden too.  
`ls -lh` it lists the file sizes but it does not list the sizes of hidden files
`ls attr` - lists the attributes 
`find ./ -type f -size 1033c` - it will find all the files(hidden too)  with size 1033 bytes under the directory and all its subsequent directories because (./) -type f : so only regular files are searched for .
Password for Level 6:
```
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```
## Level 6
The password for the next level is stored somewhere on the server and has all of the following properties:
owned by user bandit7
owned by group bandit6
33 bytes in size
So here the file is owned by some particular group and user so in the find command we will specify all that 
Commands used:
find / -user bandit7 -group bandit6 -type f - size 33c
It found a lot of files to and among them access to only one file was allowed the password was in it.
Password for level 7:
```
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```
 ## Level 7 
The password for the next level is stored in the file data.txt next to the word millionth
Command used
cat data.txt | grep millionth 
The grep command is used to identify a specific pattern or some word in a big file and highlights it in the output we can use grep for a particular name,word,symbol etc.
Password for Level 8:
```
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```
## Level 8 
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
Here sort command and uniq commands have to be used but these commands do not alter the input file and just show the output. Here comes the concept of redirecting and pipelining , but the file only had read permissions so redirecting ‘>’  is not possible as we cannot create another file and write output into that so we will use piping ‘|’ which sends output from one program(on the left) as input to another program (on the right).
Command used:
Cat data.txt | sort | uniq -u
sort  command sorts the data alphabetically and uniq-u only prints the unique line 
Password for level 9:
```
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```
## Level 9:
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
Command used:
cat data.txt | strings | grep ‘=’
The strings command will identify and print only the strings from the file. It can be used to find a particular string , string sequence etc. when used raw it returns all the strings in a file . grep will highlight the = occurring in the file 
Password for level 10 :
```
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```
## Level 10:
The password for the next level is stored in the file data.txt, which contains base64 encoded data
Command used:
cat data.txt | base64 -d
Base64 -d decodes the encoded data in base64. 
Password for level 11:
```
6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
``` 
## Level 11 
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
Here on reading the file we have that all the letters are following the sequence where each letter is moved forward 13 positions ( suppose if it is A , it will be equivalent to N ) 
Commands used:
cat data.txt 
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
tr  command will translate A-Z to N-Z and on reaching Z it will start from A-M and same with lowercase alphabets.
Password for level 12: 
```
JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```
## Level 12 
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv 

Here we will first have to create our own directory because the current directory doesn’t grant us the permission to perform changes on data.txt 
Since we are dealing with a hexdump we will firstly have to reverse it because it is a dump and in order to make it in a form so that we cant work on it , we need to reverse it.
Command used: xxd -r data.txt > data (we are reversing the hexdump and storing it in file named data)
Now we will see what kind of a file data is 
Command used: file data 
Now we get to know that data is a compressed gzip file so we will need to decompress it , in order to do that we will first have to rename the file data and give it an extension of gzip type that is gz 
Command used: mv data data.gz
Now we will decompress the file for that we have two commands gzip -d ( -d option stands for decompressing) or directly gunzip 
Command used: gzip -d data.gz
Now we will again check what is the type of the file data after being decompressed , now it turns out it is a compressed bzip2 file so we will again decompress it 
Command used: 
mv data data.bz2
gzip -d data.gz
We will keep on checking it and decompressing it 
Commands used: 
mv data data.gz
 gzip -d data.gz
Now we see that the file is tape archived so we will need to extract it 
Command used:
mv data data.tar
tar xf data5.tar
And doing the same things until the content of the file is ASCII text , we get
Password for level 13:
```
wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```
## Level 13
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on. 
In this level we have a private key stored in sshkey.private so we have to login to the next level using this private key instead of a usual password and then get the password stored in  /etc/bandit_pass/bandit14
that can be accessed by user bandit14. 
Commands Used: 
man ssh (To learn about the different options available for ssh command). 
ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private (The -i option is used for specifying the identity file . In this case the identity file sshkey.private has the private key with the help of which we got the authentication for the next level. 
After entering level 14 
cat /etc/bandit_pass/bandit14 
The password for level 14 is- 
```
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```
## Level 14 
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost. 
Here we have to connect to the port number 30000 of the localhost i.e. the machine we are working on 
Commands used- 
Here we will use the nc (netcat command) which acts like a cat command over a network. It is used for a number of reasons but here we will use its port redirecting function. Other functions are port scanning , open remote connections , port listening etc.
Syntax: 
nc <options> <hostname> <port>
here: 
we will use the connect mode of the nc command where Netcat works as a client. Which means that it establishes a connection to a remote server or servers. To work in this mode, we have to provide the `<host>` and `<port>` parameters.
```
nc localhost 30000
```
Then we will give in the password of the current level 
```
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
```
Password for level 15 is:
```
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```
## Level 15 
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
Commands used: 
openssl s_client -connect <hostname>:<port> 
(The s_client command implements a generic SSL/TLS client which connects to a remote host using SSL/TLS. It is a very useful diagnostic tool for SSL servers.)
(-connect host:port option This specifies the host and optional port to connect to) 
Here. 
```
openssl s_client -connect localhost:30001
```
After that submit the password 
```
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
```
Password for Level 16: 
```
JQttfApK4SeyHwDlI9SXGR50qclOAil1
```

