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
Попробуем закинуть в этот параметр путь до какого-нибудь другого файла:
![[Pasted image 20221204004940.png]]
Мы видим путь, характерный для windows, следовательно на машинке стоит винда.
Мы можем попробовать внедрить свой код на сайт.

Приложение запускается из корня, поэтому поднимемся на пару уровней вверх и попробуем что-нибудь прочитать:
![[Pasted image 20221204005503.png]]
Эта уязвимость называется **Local File Include**.

> На этом моменте я решил перейти на kali, чтобы не засорять себе убунту лишними утилитами.

 Далее мы будем заниматься перенаправлением трафика, а уязвимость, которую нашли, используем в качестве точки входа. 

Нам важно проверить, что responder сможет работать smb, потому что именно этот трафик мы и будем перехватывать:
![[Pasted image 20221203152337.png]]

Подрубаем responder:
![[Pasted image 20221203153526.png]]
Через флаг `-I` указывается сетевой интерфейс (в нашем случае это тунелированное соединение).

Пытаемся захватит мусорный файл через наш tun.
![[Pasted image 20221203153431.png]]
Эта уязвимость называется **Remote File Include**

И видим полученный результат в консоли:
![[Pasted image 20221203153552.png]]
Из полученного видно, что веб приложение работает как администратор на этой машинке и используется **ntlm** - протокол сетевой аутентификации, разработанный фирмой Microsoft.

**Следующая наша задача** - расшифровать полученный хэш пароля.
Запишем хэш в файл:
![[Pasted image 20221203154040.png]]

![[Pasted image 20221203154446.png]]
**john** принимает вызов/ответ NetNTLMv2 и пробует миллионы паролей, чтобы увидеть, дает ли какой-либо из них одинаковый ответ.

![[Pasted image 20221203155121.png]]

![[Pasted image 20221203155140.png]]

ea81b7afddd03efaa0945333ed147fac


