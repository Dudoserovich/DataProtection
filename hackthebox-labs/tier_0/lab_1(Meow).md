## Подключаемся к VPN

### Установка openvpn
![[Pasted image 20221203163019.png]]
### Конфигурационный файл
С помощью конфигурационного файла, скаченного с сайта, подключаемся к vpn:
![[Pasted image 20221203163215.png]]
В консоли в один момент можно увидеть следующую строчку:
```sh
2022-12-03 15:17:28 Initialization Sequence Completed
```
Это значит, что всё хорошо и мы подключились.

## А что, а как?
Используется так называемое **туннелирование** (от англ. tunnelling — «прокладка туннеля») в компьютерных сетях — процесс, в ходе которого создаётся логическое соединение между двумя конечными точками посредством инкапсуляции различных протоколов.

По факту мы оказываемся во внутренней сети _hackthebox_.

## Отвечаем на вопросики
Один из вопросов, который есть на сайте - "What is the abbreviated name for a 'tunnel interface' in the output of your VPN boot-up sequence output?"
Чтобы ответить на этот вопрос пишем `ifconfig` в консоли.
![[tun_ip_addres.png]]
Эта сеть тунелирует наше соединение с целевой машиной.
**Ответ на вопрос:** tun

### Проверяем пульс машинки
![[Pasted image 20221203164901.png]]
> P.S. флаг `c3`  говорит о том, что мы пингуем только 3 раза.

### Доступные порты
![[Pasted image 20221203165336.png]]
Машинка жива и мы видим доступный tcp порт 23, а значит мы может подклюситься к машинке с помощью **telnet** (при nmap указан именно этот сервис).

### Конектимся с машинкой
На сайте мы узнаем, что пользователь, под которым мы будем заходить - **root**.

Заходим под рутом и читаем содержимое файла, которое нам нужно для одного из последних заданий:
![[Pasted image 20221203165901.png]]