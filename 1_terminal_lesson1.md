# Домашнее задание к занятию "Работа в терминале. Лекция 1"


## Задание

>1. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

>	* Создайте директорию, в которой будут храниться конфигурационные файлы Vagrant. В ней выполните `vagrant init`. Замените содержимое Vagrantfile по умолчанию >следующим:

		```bash
		Vagrant.configure("2") do |config|
			config.vm.box = "bento/ubuntu-20.04"
		end
		```

>	* Выполнение в этой директории `vagrant up` установит провайдер VirtualBox для Vagrant, скачает необходимый образ и запустит виртуальную машину.

>	* `vagrant suspend` выключит виртуальную машину с сохранением ее состояния (т.е., при следующем `vagrant up` будут запущены все процессы внутри, которые >работали на момент вызова suspend), `vagrant halt` выключит виртуальную машину штатным образом.

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_9.png "Suspended")

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_8.png "Suspended")

>2. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей >выделены. Какие ресурсы выделены по-умолчанию?

**ВМ по-умолчанию создалась с 1Гб памяти, 2 ядрами ЦПУ, и диском 64Гб (тонкий, реальный размер пока 1,89Гб).**
![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_10.png "Ресурсы")

>3. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: [документация](https://www.vagrantup.com/docs/providers/virtualbox/configuration.html). Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

**Чтобы изменить настройки ВМ нужно отредактировать файл Vagrantfile и добавить, например, такие строки, чтобы переименовать ВМ и выдать 4 ЦПУ и 4Гб памяти:**

 ``` 
 config.vm.provider "virtualbox" do |vb|
    vb.name = "Julls_VM"
    vb.memory = 4096
    vb.cpus = 4
  end
  ```

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_11.png "Конфиг")
![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_14.png "Ресурсы")

>4. Команда `vagrant ssh` из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. >Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_12.png "Команды")
![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_13.png "Команды")

>5. Ознакомьтесь с разделами `man bash`, почитайте о настройках самого bash:
   * какой переменной можно задать длину журнала `history`, и на какой строчке manual это описывается?

**У меня показал 846 строку, HISTFILESIZE:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_16.png "Переменные")

 >   * что делает директива `ignoreboth` в bash?

**Позволяет игнорировать и пробелы, и дублирующиеся строки**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_15.png "Переменные")

>6. В каких сценариях использования применимы скобки `{}` и на какой строчке `man bash` это описано?

**На строчке 248 начинается описание команд. {} используется для создания списков**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_17.png "Скобки")

>7. С учётом ответа на предыдущий вопрос, как создать однократным вызовом `touch` 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

**Можно командой touch создать список файлов, указать диапазоном:**
 ```
touch {1..100000}
 ```
![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_18.png "Стотыщфайлов")

**300000 не создалось, явно мешает значение какое-то переменной. Гугл подсказал, что это ARG_MAX (увеличить ограничение на объём передаваемых аргументов комманде). Менять его я, конечно, не буду :)**

>8. В man bash поищите по `/\[\[`. Что делает конструкция `[[ -d /tmp ]]`

**Поиск по \[\[ привел меня к:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_20.png "экспрешнэкспрешн")

**Конструкция, судя по описанию, должна выводить 1 или 0, если есть или нет такой директории, но у меня почему-то ничего не выводит**

**Нашла вот такую конструкцию:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_21.png "экспрешнэкспрешн")

 **меняем вывод результата проверки и снова запускаем, директория найдена!**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_22.png "экспрешнэкспрешн")

*UPD доработка*

**Я понимаю, что он возвращать должен 0, если проверяемое выражение - истина (в нашем случае если директория существует), 1, если выражение - ложь. Но оно не выводил ничего, поэтому и изобрела ту конструкцию натягивания совы на глобус.**

**Спросила Сергея на вебинаре о выводе на экран результата выполнения и он подсказал как сделать эхо, чтоб оно отработало:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_5.png "эхо")

>9. Сделайте так, чтобы в выводе команды `type -a bash` первым стояла запись с нестандартным путем, например bash is ... 
Используйте знания о просмотре существующих и создании новых переменных окружения, обратите внимание на переменную окружения PATH 

	```bash
	bash is /tmp/new_path_directory/bash
	bash is /usr/local/bin/bash
	bash is /bin/bash
	```

>	(прочие строки могут отличаться содержимым и порядком)
>    В качестве ответа приведите команды, которые позволили вам добиться указанного вывода или соответствующие скриншоты.

**Смотрим что отображается сейчас:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_25.png "path")

**Копируем файлик в нужную новую директорию и правим PATH:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_23.png "path")

**ИИИИИ не работает :) Поняла где ошиблась, исправила:**

![Скрин](https://github.com/Jlljully/terminal-OS-net-security/blob/main/files/lesson_1/Screenshot_24.png "path")

>10. Чем отличается планирование команд с помощью `batch` и `at`?

**at используется для выполнения однократного задания в заданное время, а команда batch — для назначения одноразовых задач, которые должны выполняться, когда загрузка низкая**

11. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.
