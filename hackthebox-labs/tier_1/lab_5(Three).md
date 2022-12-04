## ping
![[Pasted image 20221204015937.png]]

## nmap
Результат nmap:
```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 17:8b:d4:25:45:2a:20:b8:79:f8:e2:58:d7:8e:79:f4 (RSA)
|   256 e6:0f:1a:f6:32:8a:40:ef:2d:a7:3b:22:d1:c7:14:fa (ECDSA)
|_  256 2d:e1:87:41:75:f3:91:54:41:16:b7:2b:80:c6:8f:05 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: The Toppers
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

## Сам сайт
![[Pasted image 20221204020720.png]]

Почтовый ящик расположен на личном домене, значит могут быть другие поддомены.
![[Pasted image 20221204020753.png]]

Добавим ip сайта в локальный файл DNS (`/etc/hosts`)
![[Pasted image 20221204021259.png]]

![[Pasted image 20221204021432.png]]

## gobuster
![[Pasted image 20221204021537.png]]

![[Pasted image 20221204021710.png]]

Мы хотим узнать располагаются ли ещё какие-нибудь домены на машинке.
Используем всё тот же gobuster и режим **vhost** для этого и словарь secrets с поддоменами.
![[Pasted image 20221204043834.png]]

Среди кучи муссорных поддоменов есть один интересный: **s3**

Добавим его в файл `/etc/hosts`:
![[Pasted image 20221204044050.png]]

Что мы видим на этом поддомене:
![[Pasted image 20221204044316.png]]

aws имеет свой интерфейс командной строки, с которым мы можем взаимодействовать (awscli).
aws часто не проверяет содержимое ключей, поэтомы мы можем закидать в него какой-нибудь мусор.

