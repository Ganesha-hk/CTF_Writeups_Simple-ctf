<p align="center">
  <img src="https://repository-images.githubusercontent.com/518509014/f7450454-158c-45e0-8b38-0c0ae4d7394c" width="800">
</p>
<p align="center">
<img src="https://readme-typing-svg.herokuapp.com?color=00FF00&size=35&center=true&vCenter=true&width=1000&lines=Offensive+Security+Writeups;TryHackMe+%7C+HackTheBox+%7C+CTF;Cybersecurity+Learning+Journey;Enumeration+%7C+Exploitation+%7C+Privilege+Escalation">
</p>

---

<h1 align="center">⚡ Offensive Security CTF Writeups ⚡</h1>

<p align="center">
<img src="https://img.shields.io/badge/Focus-Offensive%20Security-red">
<img src="https://img.shields.io/badge/Platform-TryHackMe-green">
<img src="https://img.shields.io/badge/Tools-Nmap%20%7C%20FFUF%20%7C%20BurpSuite-blue">
<img src="https://img.shields.io/badge/Status-Active%20Learning-success">
</p>

<p align="center">
<img src="https://img.shields.io/badge/Linux-Privilege%20Escalation-black">
<img src="https://img.shields.io/badge/Web-SQL%20Injection-orange">
<img src="https://img.shields.io/badge/CTF-Writeups-purple">
</p>

---

> “The quieter you become, the more you are able to hear.”  
> — Kali Linux Philosophy

---
<p align="center">
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:000000,100:00ff00&height=200&section=header&text=CTF%20Writeups&fontColor=00ff00&fontSize=50&animation=fadeIn" />
</p>


## Eumeration


1 : nmap scan
    
    -> nmap -sC -sV -A 10.x.x.x
    -> open ports 2
     - 80 = http
     - 2222 = ssh
    -> OS = Linux(ubuntu)
    
<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/enu.jpeg?raw=true" height="400"> 

2 : ffuf

    ->command: ffuf -w /home/haxxx/SecLists/Discovery/Web-Content/common.txt -u http://X0.X8.1X1.1X2/FUZZ
    -> the hidden directorys are:
    -> /simple

<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ffuf.jpeg?raw=true" height="400">


## Initial Access


There is a cms-made-simple cms-website is running on port 80 /simple hidden directry
if we serearch a vulnerabitlity for cms-made-simple in exploit-db then we get sqli of
CVE-2019-9053 where these python script is made for python2 version so run in any low linux
system or in thm attackbox

<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ap4.jpeg?raw=true" height="400">
<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ap5.jpeg?raw=true" height="400">

    ->python2 exploit.py -u http://10.x.x.x/simple --crack -w /home/kali/rockyou.txt

then we get username,salt,emal and password 

<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ap3.jpeg?raw=true" height="400">

now connect to ssh useing command

    ->sudo ssh mitch@10.x.x.x -p 2222
    -p(port 2222) because ssh is running on port 2222
    

<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ap2.jpeg?raw=true" height="400">

we get initial access

<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ap1.jpeg?raw=true" height="400">


## Privelege Esculation


now run sudo -l then we get output says /user/bin/vim can be run as root without password
so useing caommand

    -> sudo vim -c ':!/bin/sh -p'
    
we get root shell and root flag


<img src="https://github.com/Ganesha-hk/CTF_Writeups_Simple-ctf/blob/main/Simple-ctf/Images/ap6.jpeg?raw=true" height="400">


## 📚 Lessons Learned


so dont use low version cms websites or better not use cms websites and make the website 
database secure so that sqli not happen and sudo misconfiguration can lead to root access so
do cross check that no file has sudo no password permesion.

## ⚠ Disclaimer

These writeups are created for educational purposes only.  
Do not use techniques described here on systems without authorization.