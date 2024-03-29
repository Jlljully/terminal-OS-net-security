# Домашнее задание к занятию «Операционные системы. Лекция 2»


1. На лекции вы познакомились с [node_exporter](https://github.com/prometheus/node_exporter/releases). В демонстрации его исполняемый файл запускался в background. Этого достаточно для демо, но не для настоящей production-системы, где процессы должны находиться под внешним управлением. Используя знания из лекции по systemd, создайте самостоятельно простой [unit-файл](https://www.freedesktop.org/software/systemd/man/systemd.service.html) для node_exporter:

    * поместите его в автозагрузку;
    * предусмотрите возможность добавления опций к запускаемому процессу через внешний файл (посмотрите, например, на `systemctl cat cron`);
    * удостоверьтесь, что с помощью systemctl процесс корректно стартует, завершается, а после перезагрузки автоматически поднимается.

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_2.png "1")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_4.png "2")

**Стоп-старт работают без проблем**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_5.png "3")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_6.png "4")

2. Изучите опции node_exporter и вывод `/metrics` по умолчанию. Приведите несколько опций, которые вы бы выбрали для базового мониторинга хоста по CPU, памяти, диску и сети.

### Ответ

**node_scrape_collector_duration_seconds{collector="cpu"} 0.000342195  
node_scrape_collector_duration_seconds{collector="cpufreq"} 4.7937e-05  
node_scrape_collector_duration_seconds{collector="diskstats"} 0.00032759  
node_scrape_collector_duration_seconds{collector="meminfo"} 0.000134224  
node_scrape_collector_duration_seconds{collector="netstat"} 0.001132181**  

3. Установите в свою виртуальную машину [Netdata](https://github.com/netdata/netdata). Воспользуйтесь [готовыми пакетами](https://packagecloud.io/netdata/netdata/install) для установки (`sudo apt install -y netdata`). 
   
   После успешной установки:
   
    * в конфигурационном файле `/etc/netdata/netdata.conf` в секции [web] замените значение с localhost на `bind to = 0.0.0.0`;
    * добавьте в Vagrantfile проброс порта Netdata на свой локальный компьютер и сделайте `vagrant reload`:

    ```bash
    config.vm.network "forwarded_port", guest: 19999, host: 19999
    ```

    После успешной перезагрузки в браузере на своём ПК (не в виртуальной машине) вы должны суметь зайти на `localhost:19999`. Ознакомьтесь с метриками, которые по умолчанию собираются Netdata, и с комментариями, которые даны к этим метрикам.

### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_7.png "5")

4. Можно ли по выводу `dmesg` понять, осознаёт ли ОС, что загружена не на настоящем оборудовании, а на системе виртуализации?

### Ответ

**Да, можно:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_8.png "dmesg")

5. Как настроен sysctl `fs.nr_open` на системе по умолчанию? Определите, что означает этот параметр. Какой другой существующий лимит не позволит достичь такого числа (`ulimit --help`)?

### Ответ

**Это - хардлимит на количество дескрипторов (запущенных файлов). Есть еще софтлимит, посмотреть его можно uname -n**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_10.png "fs.nr_open")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_11.png "fs.nr_open")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_12.png "fs.nr_open")

6. Запустите любой долгоживущий процесс (не `ls`, который отработает мгновенно, а, например, `sleep 1h`) в отдельном неймспейсе процессов; покажите, что ваш процесс работает под PID 1 через `nsenter`. Для простоты работайте в этом задании под root (`sudo -i`). Под обычным пользователем требуются дополнительные опции (`--map-root-user`) и т. д.

### Ответ

**Запустила для примера просто /bin/bash и топ**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_14.png "unshare")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_13.png "unshare")

7. Найдите информацию о том, что такое `:(){ :|:& };:`. Запустите эту команду в своей виртуальной машине Vagrant с Ubuntu 20.04 (**это важно, поведение в других ОС не проверялось**). Некоторое время всё будет плохо, после чего (спустя минуты) — ОС должна стабилизироваться. Вызов `dmesg` расскажет, какой механизм помог автоматической стабилизации.  
Как настроен этот механизм по умолчанию, и как изменить число процессов, которое можно создать в сессии?

*В качестве решения отправьте ответы на вопросы и опишите, как эти ответы были получены.*


### Ответ

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_17.png "unshare")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_4/Screenshot_19.png "unshare")
 
**Оно так и не отработало. Сначала на машине, я подумала, было больно много ресурсов - уменьшила и запустила еще раз. Больше полутора часов я ждала, но решила ребутнуть ВМ и становить этот странный эксперимент. За это время нагулилось уже все что могло произойти: эта штука форкает бесконечно процессы, забивая ресурсы. В какой-то момент должно было наступить или исчерпание дескрипторов (тот самый софт лимит из пункта выше) или вступить oom-killer после исчерпания ресурсов памяти. Но если CPU у меня забился полностью, то память успешно сбрасывала лишнее в своп и ни о чем не беспокоилась  
-_-**

**Самое неплохое описание, что я встретила, как он работает:**

>На самом деле OOM Killer использует достаточно сложный анализ и присваивает каждому процессу очки негодности (badness) и при исчерпании памяти будет убит не кто-попало, а самый негодный процесс. Очки негодности могут принимать значения от -1000 до 1000, чем выше значение, тем более высока вероятность что OOM Killer убьет процесс. Процесс с -1000 очков никогда не будет убит OOM Killer.  

>Как вычисляются очки негодности? За основу берется процент физической памяти используемый процессом и умножается на 10, таким образом получаем базовое значение. Нетрудно заметить, что 1000 очков - это 100% использования памяти.   

**Еще вариант - поменять софтлимит, чтоб быстрее утыкался в лимит, правда, я не уверена, что это точно сработает:  
uname -u 300**
