В этой лабораторной будет рассмотрен web-сервер **Apache**.
## nmap
![[Pasted image 20221203192427.png]]
## Сам сайт
Видим, что апач слушает 80 порт, значит мы можем просто в браузере перейти на этот сайт:
![[Pasted image 20221203194822.png]]
Видим, что нам нужно авторизоваться, поэтому попробуем авторизоваться с помощью sql-иньекции. И так как форма отправляет **post запрос**, то в адресную строку вбить данные мы не можем, будем пытаться что-то закинуть прямо в поле логина и пароля.

_А именно:_
**login:** `admin' or 1=1 #`
Логика следующая: `login = 'admin' or 1=1`, а часть с паролем комментируется(`#`), поэтому **password:** любой

**Результат:**
![[Pasted image 20221203194734.png]]
Наши старания награждены флагом