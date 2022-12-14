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
Скорее всего это так называемый **Amazon Simple Storage Service** _(aws s3)_ — онлайн веб-служба, предлагаемая Amazon Web Services, предоставляет возможность хранения и получения любого объёма данных в любое время из любой точки сети, так называемый файловый хостинг.

**Добавим этот хост в файл `/etc/hosts`:**
![[Pasted image 20221204044050.png]]

**Что мы видим на этом поддомене:**
![[Pasted image 20221204044316.png]]
> status запущено, значит всё круто, как нам говорит hackthebox.

**aws** имеет свой интерфейс командной строки, с которым мы можем взаимодействовать (**awscli**).
**aws** часто не проверяет содержимое ключей, поэтомы мы можем закидать в него какой-нибудь мусор.
![[VirtualBoxVM_gIE3tZQnWZ.png]]

Далее мы посмотрим какие bucket (вёдра) есть на сервере.
> **endpoint** - урл, на котором расположен сервис s3
> **s3** - interact w/ s3 service
> **ls** - list bucket names

![[Pasted image 20221204154926.png]]
> Мы видим, что у нас есть файл index.php
> Это значит, что весь сайт размещается именно отсюда, с этого ведра s3

![[Pasted image 20221204163150.png]]

### Команда ls
![[VirtualBoxVM_ZQbH0Gw9Aw.png]]

### Команда id
![[RsqdXAjSjc.png]]

## Создаём обратную оболочку
![[Pasted image 20221204170140.png]]
`&>` проверяет открыт ли дескриптор целевого файла для вывода.
`/dev/tcp` является особым случаем bash, он открывает сокет (который затем ведёт себя как обычный дескриптор файла по отношению к вызовам чтения и записи). Сокет позволяет как чтение, так и запись.
`0` -стандартный поток ввода.
`0>&1` перенаправляем стандартный поток ввода на стандартный поток вывода. 
**Соокет** — название программного интерфейса для обеспечения обмена данными между процессами.
![[Pasted image 20221204170107.png]]
![[Pasted image 20221204170046.png]]
![[Pasted image 20221204170217.png]]
> **Что вообще произошло?**
> На порту 8000 у нас лежит скрипт, который позволит нам на порту 1337 нашего сервера получить оболочку атакуемой машинки.

**Скрипт получен успешно:**
![[Pasted image 20221204170019.png]]

**Обратная оболочка в деле:**
![[Pasted image 20221204165939.png]]
> Ну и наш флаг уже лежит там в ожидании