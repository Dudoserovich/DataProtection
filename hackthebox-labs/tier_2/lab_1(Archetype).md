## Результат nmap
```
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Windows Server 2019 Standard 17763 microsoft-ds
1433/tcp open  ms-sql-s     Microsoft SQL Server 2017 14.00.1000.00; RTM
| ms-sql-ntlm-info: 
|   Target_Name: ARCHETYPE
|   NetBIOS_Domain_Name: ARCHETYPE
|   NetBIOS_Computer_Name: ARCHETYPE
|   DNS_Domain_Name: Archetype
|   DNS_Computer_Name: Archetype
|_  Product_Version: 10.0.17763
|_ssl-date: 2022-12-04T10:54:36+00:00; +1h00m00s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-12-04T07:04:03
| Not valid after:  2052-12-04T07:04:03
| MD5:   43fb e442 1ed7 1ead d666 f70b 5d14 c611
|_SHA-1: b83d 5d16 8c63 a865 c509 3666 d3f6 6527 be16 ffa7
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2022-12-04T10:54:24
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows Server 2019 Standard 17763 (Windows Server 2019 Standard 6.3)
|   Computer name: Archetype
|   NetBIOS computer name: ARCHETYPE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2022-12-04T02:54:28-08:00
| ms-sql-info: 
|   10.129.150.203:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM
|       number: 14.00.1000.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
|_clock-skew: mean: 2h36m01s, deviation: 3h34m42s, median: 59m59s
```
Из интересного, тут снова присутствует samba, а так же ms sql сервер.

## Посмотрим что там на общих ресурсах samba
![[Pasted image 20221204200530.png]]
Почти все общие ресурсы предназначены для администраторов, кроме **backups**.

![[Pasted image 20221204200806.png]]

![[Pasted image 20221204200843.png]]

```xml
<DTSConfiguration>
    <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="..." GeneratedFromPackageName="..." GeneratedFromPackageID="..." GeneratedDate="20.1.2019 10:01:34"/>
    </DTSConfigurationHeading>
    <Configuration ConfiguredType="Property" Path="\Package.Connections[Destination].Properties[ConnectionString]" ValueType="String">
        <ConfiguredValue>Data Source=.;Password=M3g4c0rp123;User ID=ARCHETYPE\sql_svc;Initial Catalog=Catalog;Provider=SQLNCLI10.1;Persist Security Info=True;Auto Translate=False;</ConfiguredValue>
    </Configuration>
</DTSConfiguration>
```

Тут присутсвует пароль пользователя `ARCHETYPE\sql_svc`.
`Password=M3g4c0rp123;User ID=ARCHETYPE\sql_svc;`

## ms sql
Проверим другую службу с помощью полученного логина и пароля.
![[Pasted image 20221204202446.png]]
Ура, всё прокнуло, но что же мы тут можем делать?
![[Pasted image 20221204203245.png]]
А мы можем испольнять консольные команды прямо отсюда, попробуем сделать что-нибудь плохое.

Запустим у себя веб сервер и попытаемся скачать netcat на атакуемую машинку.
![[Pasted image 20221204204119.png]]
![[Pasted image 20221204204144.png]]
![[Pasted image 20221204204327.png]]

Теперь будем пытаться войти в оболочку на нашей локальной машинке:
![[VirtualBoxVM_941HHPu50f.png]]
![[Pasted image 20221204204652.png]]
Круто, всё получилось. Мы отправили с помощью netcat оболочку на машинку, которая слушала порт.

Ищем ключик:
![[Pasted image 20221204205103.png]]
Ключик пользователя: `3e7b102e78218e935bf3f4951fec21a3`

## Повышение привелегий
Сейчас нам нужно повысить привелегии, чтобы получить ещё и root ключик.
Я скачал скрипт для повышения привелегий себе на машинку, осталось всего-то запустить его на атакуемой:
![[Pasted image 20221204210412.png]]

Снова запускаем веб сервер:
![[Pasted image 20221204210447.png]]

И через консоль, в которой мы уже сидим по виндой, качаем скрипт
![[Pasted image 20221204211827.png]]
![[Pasted image 20221204211941.png]]
Файл скачен, теперь запускаем и видим вывод в виде огромной партянки:
![[Pasted image 20221204212240.png]]
Красным отмечено то, на что нам стоит обратить внимание и сразу же видно, что файл `C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt` встречается несколько раз, проверим его.

Похоже, что внутри лежит логин с паролем для администратора:
![[Pasted image 20221204212513.png]]
`/user:administrator MEGACORP_4dm1n!!`
Заходим под этим пользователем через evil-winrm:
![[Pasted image 20221204213847.png]]
**evil-winrm** - по факту даёт удаленное управление Windows, но только консольное. Используется для хакинга и пентеста.
Приватный ключик найден: `b91ccec3305e98240082d4474b848528`