# OTUS ДЗ Почта SMTP, IMAP, POP3, Postfix, Dovecot  (Centos 7)
----------------------------------------------------------------------- 

```
Домашнее задание
Установка почтового сервера
Цель: В результате выполнения ДЗ студент установит почтовый сервер.
1. Установить в виртуалке postfix+dovecot для приёма почты на виртуальный домен любым обсужденным на семинаре способом
2. Отправить почту телнетом с хоста на виртуалку
3. Принять почту на хост почтовым клиентом

Результат
1. Полученное письмо со всеми заголовками
2. Конфиги postfix и dovecot
```

### Как запустить:
- git clone git@github.com:staybox/otus_dz25.git && cd otus_dz25 && vagrant up

### Как проверить:

1. С вашего хоста выполнить ```telnet localhost 20025``` и ```telnet localhost 20143```, это проверка SMTP и IMAP портов. 

- Далее пробуем отправить письмо через telnet:

![Image 1](https://raw.githubusercontent.com/staybox/otus_dz25/master/screenshots/telnet.png)

Команды для подключение к SMTP:
```
telnet localhost 20025

    helo mailserver.otus.local
    mail from: test@example.com
    rcpt to: vagrant@mailserver.otus.local
    data
    Subject: This is subject of my email
    This is body
    .
```

- Заходим на сервер и видим в файле журнала postfix что письмо было положено в почтовый ящик:

 ![Image 2](https://raw.githubusercontent.com/staybox/otus_dz25/master/screenshots/maillog.png)

- Далее мы можем подключиться через telnet по IMAP и посмотреть наше письмо в почтовом ящике:

 ![Image 3](https://raw.githubusercontent.com/staybox/otus_dz25/master/screenshots/dovecot.png)

 Команды для подключения к Dovecot:
 ```
 telnet localhost 20143
    a login vagrant password
    b select inbox
    b UID SEARCH *
    a UID FETCH 1 (BODY.PEEK[1.MIME])
 ```

- Теперь мы запускаем дефолтный почтовый клиент в Centos 7 и пробуем прочитать наше письмо, а также отправить с помощью почтового клиента письмо:

 ![Image 4](https://raw.githubusercontent.com/staybox/otus_dz25/master/screenshots/evo.png)

 ![Image 5](https://raw.githubusercontent.com/staybox/otus_dz25/master/screenshots/evo2.png)
