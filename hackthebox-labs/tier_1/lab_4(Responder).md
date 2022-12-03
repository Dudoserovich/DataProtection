## ping
![[Pasted image 20221203223007.png]]

## nmap
Результат работы nmap:
```bash
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).

```

![[Pasted image 20221203223309.png]]

Изменим файлик `/etc/hosts`, добавим новый домен (unika.htb) для адреса _10.129.87.25_:
![[Pasted image 20221203224005.png]]

Это сработало:
![[Pasted image 20221203223942.png]]
Сайт представляет из себя _landing_.

При переключении языка меняется адресная строка:
![[Pasted image 20221203224435.png]]
Мы прям видим **get** параметр с адресом html страницы и главный файл (точку входа) `index.php`
Попробуем закинуть в этот параметр какой-нибудь другой файл:
![[Pasted image 20221204004940.png]]
Мы видим путь, характерный для windows, следовательно на машинке стоит винда.
Мы можем попробовать внедрить свой код на сайт.

Приложение запускается из корня, поэтому поднимемся на пару уровней вверх и попробуем что-нибудь прочитать:
![[Pasted image 20221204005503.png]]
...

Так же потенциально интересным является форма обратной связи:
![[Pasted image 20221203224558.png]]
Можно будет проверить присутствуют ли на сайте sql иньекции.


