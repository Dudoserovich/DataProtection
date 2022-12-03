`-sC` позволяет получить дополнительную информацию о службах и является флагом поумолчанию
## ping
![[Pasted image 20221203212926.png]]

## nmap
Результат map:
```bash
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 ftp      ftp            33 Jun 08  2021 allowed.userlist
|_-rw-r--r--    1 ftp      ftp            62 Apr 20  2021 allowed.userlist.passwd
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.109
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: 1248E68909EAE600881B8DB1AD07F356
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Smash - Bootstrap Business Template
Service Info: OS: Unix

```
## ftp
![[Pasted image 20221203213918.png]]

Мы нашли файлы с логинами и пароялми, сохраним их себе на локалку:
![[Pasted image 20221203213936.png]]

## apache
![[Pasted image 20221203213729.png]]

## gobuster
т.к. лабы выполнялись на убунте, пришлось скачать словари для брутфорса и поставить сам gobuster. 
![[Pasted image 20221203221032.png]]
**gobuster** сам по себе позволяет искать файлы и директории по папкам сразу нескольких расширений вебсайта.
Командой, введённой вышел, мы говорим, что будем искать на таком-то сайте, с помощью такого-то словаря, файлы с такими-то расширениями.

Мы видим 200 status code для `index.html`, `login.php` и `config.php`
Попробуем перейти на `login.php`

## Проверка найденных путей
Мы попали на страницу авторизации, попробуем использовать полученный по ftp логины и пароли (войдём под админом)
![[Pasted image 20221203221859.png]]

Удалось войти под админом и тут нас встречает необходимый flag.
![[Pasted image 20221203221827.png]]