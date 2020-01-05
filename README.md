# PAM practice
In this project, we configure PAM module to allow only users in UNIX group `admin` to have possibility to ssh all week long.
Other users can access only on work days.
# Run  
0) `vagrant` and should be installed on your system
```
$ vagrant -v
Vagrant 2.2.5
```
1) Clone this repository
```bash  
$ git clone https://github.com/ligain/pam.git  
``` 
2) Go to project folder
```bash  
$ cd pam/
```  
3) Run `Vagrantfile`
```bash  
$ vagrant up
```
4) Try to connect via ssh to VM as `user1` and `admin1` using  a password **Otus2020**.
You will see similar output on weekend:
```
$ ssh admin1@127.1 -p 2222 
...
admin1@127.1's password: 
[admin1@localhost ~]$ logout
Connection to 127.1 closed.
$ ssh user1@127.1 -p 2222 
user1@127.1's password: 
Connection to 127.1 closed by remote host.
Connection to 127.1 closed.
```
