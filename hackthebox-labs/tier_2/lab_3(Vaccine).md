## Результат nmap
```
PORT      STATE    SERVICE VERSION
21/tcp    open     ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rwxr-xr-x    1 0        0            2533 Apr 13  2021 backup.zip
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.45
|      Logged in as ftpuser
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp    open     ssh     OpenSSH 8.0p1 Ubuntu 6ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 c0:ee:58:07:75:34:b0:0b:91:65:b2:59:56:95:27:a4 (RSA)
|   256 ac:6e:81:18:89:22:d7:a7:41:7d:81:4f:1b:b8:b2:51 (ECDSA)
|_  256 42:5b:c3:21:df:ef:a2:0b:c9:5e:03:42:1d:69:d0:28 (ED25519)
80/tcp    open     http    Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: MegaCorp Login
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.41 (Ubuntu)
27355/tcp filtered unknown
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```
**Сервисы:** ftp, ssh, apache
На ftp мы видим файл backup, попробуем вытащить его.

## ftp
![[Pasted image 20221205005542.png]]

Чтобы вытащить содержимое архива необходим пароль:
![[Pasted image 20221205005855.png]]
Ну, как говорится брутфорс - наше всё, поэтому используем Джона Потрошителя для подбора пароля:
![[Pasted image 20221205010651.png]]
![[Pasted image 20221205010617.png]]

Распаковываем содержимое:
![[Pasted image 20221205010746.png]]

Для отправки формы испольется post запрос:
![[Pasted image 20221205010923.png]]
Ожидается, что логин - `admin`, а пароль это хэш md5(самый херовый выбор если честно), равный строке - `2cb42f8734ea607eefed3b70af13bbd3`.
Дешифровать md5 не составит особых проблем.

Будем использовать hashcat:
![[Pasted image 20221205012816.png]]
Возникли определённые трудности с hashcat на виртуалке, поэтому я попытался сделать тоже самое с wsl Ubuntu:
![[Pasted image 20221205012740.png]]
> Пароль: `qwerty789`

## Сайт
![[Pasted image 20221205005105.png]]

Мы успешно зашли:
![[Pasted image 20221205013018.png]]



