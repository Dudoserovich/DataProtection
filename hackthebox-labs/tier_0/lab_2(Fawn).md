**ip addres machine:** 10.129.248.150

## Проверяем пульс машинки
![[Pasted image 20221203170423.png]]
Она жива, всё хорошо.

## nmap
![[Pasted image 20221203170631.png]]
- Флаг `-sV` выводит версии сервисов.
- Флаг `-sC` говорит нам показывать допольнительную ифнормацию.
- Флаг `-v` говорит о повышении уровня вербальности. Это значит, что по мере выполнения скрипта nmap будет выплёвывать доступные порты и прочую шелуху.

Видим наш **ftp** сервис, открытый на 21 порту:
![[Pasted image 20221203170619.png]]
Тут есть вся необходимая информация о версии ftp - vsftpd (в консоли видно, что **vsFTPd 3.0.3** - защищённый, быстрый и стабильный)
**Операционка сервиса** - unix
Так же мы видим аннонимного пользователя, под которым мы и будет подключаться - **Anonymous**

## Входим в систему по ftp
![[Pasted image 20221203171542.png]]
**Логин:** _Anonymous_
Его мы выяснили в предыдущем шаге, пароль пустой, просто жмём _enter_.
Качаем себе файл с помощью **get** и проверяем содержимое на своём пк.

