# Домашнее задание к занятию «Компьютерные сети. Лекция 1»


**Шаг 1.** Работа c HTTP через telnet.

- Подключитесь утилитой telnet к сайту stackoverflow.com:

`telnet stackoverflow.com 80`
 
- Отправьте HTTP-запрос:

```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
*В ответе укажите полученный HTTP-код и поясните, что он означает.*

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_2.png "telnet")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_3.png "telnet")

```
HTTP 403 Forbidden — стандартный код ответа HTTP, означающий, что доступ к запрошенному ресурсу запрещен. Сервер понял запрос, но не выполнит его. Наиболее вероятными причинами ограничения может послужить попытка доступа к системным ресурсам веб-сервера (например, файлам .htaccess или .htpasswd) или к файлам, доступ к которым был закрыт с помощью конфигурационных файлов, требование аутентификации не средствами HTTP, например, для доступа к системе управления содержимым или разделу для зарегистрированных пользователей либо сервер не удовлетворён IP-адресом клиента, например, при блокировках. Появился в HTTP/1.0.
```

**если зайти на сайт и обратить внимание на адрес, то становится понятно, что они перешли на https, поэтому запрос не может быть выполнен - телнет не может с шифрованием работать**

**Шаг 2.** Повторите задание 1 в браузере, используя консоль разработчика F12:

 - откройте вкладку `Network`;
 - отправьте запрос [http://stackoverflow.com](http://stackoverflow.com);
 - найдите первый ответ HTTP-сервера, откройте вкладку `Headers`;
 - укажите в ответе полученный HTTP-код;
 - проверьте время загрузки страницы и определите, какой запрос обрабатывался дольше всего;
 - приложите скриншот консоли браузера в ответ.

### Ответ

**Код 307 - редирект:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_4.png "F12")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_5.png "F12")

**Самый долгий запрос выполнялся 297мс, если его развернуть, то увидим, что это GET**

**Шаг 3.** Какой IP-адрес у вас в интернете?

### Ответ

**Так как он статичный, не хочу показывать**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_6.png "IP")

**Шаг 4.** Какому провайдеру принадлежит ваш IP-адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`.

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_7.png "whois")

**Шаг 5.** Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`.

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_8.png "whois")

**Шаг 6.** Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка — delay?

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_9.png "mtr")

**Самая большая задержка на 7-9 хопах - уже у гугла, если посмотреть AS**

**Шаг 7.** Какие DNS-сервера отвечают за доменное имя dns.google? Какие A-записи? Воспользуйтесь утилитой `dig`.

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_10.png "dig")

**Шаг 8.** Проверьте PTR записи для IP-адресов из задания 7. Какое доменное имя привязано к IP? Воспользуйтесь утилитой `dig`.

*В качестве ответов на вопросы приложите лог выполнения команд в консоли или скриншот полученных результатов.*

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_6/Screenshot_11.png "dig")
