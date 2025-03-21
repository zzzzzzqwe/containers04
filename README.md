# Лабораторная работа №4. Использование контейнеров как среды выполнения

## Студент
**Gachayev Dmitrii I2302**  
**Выполнено 10.03.2025**  

## Цель работы
Данная лабораторная работа призвана напомнить основные команды ОС Debian/Ubuntu. Также она позволит познакомиться с Docker и его основными командами.
## Задача
Запустить контейнер Ubuntu, установить Web-сервер Apache и вывести в браузере страницу с текстом "Hello, World!".
## Выполнение работы
1. Открываю терминал в папке `containers04` и выполняю команду:

```bash
docker run -ti -p 8000:80 --name containers04 ubuntu bash
```

Эта команда запускает новый контейнер Docker на основе образа Ubuntu и выполняет в нем bash (терминал).

Параметры команды:

- `docker run` – создает и запускает новый контейнер.
- `ti` - выделяет псевдотерминал, позволяет взаимодействовать с контейнером в интерактивном режиме
- `p 8000:80` - Перенаправляет порт 80 контейнера (где работает Apache) на порт 8000 хостовой машины. Позволяет открывать сайт в браузере по адресу `localhost:8000`
- `--name containers04` - Задает имя контейнера containers04
- `ubuntu` - Использует официальный образ Ubuntu в качестве ОС контейнера.
- `bash` - Запускает командную оболочку Bash внутри контейнера.


В консоль выводится следующее:

![image](screenshots/Screenshot_1.png)


2. В открывшемся окне выполняю команды:

`apt update` - обновляет список доступных пакетов и их версий.

- `APT (Advanced Package Tool)` получает актуальную информацию о пакетах из репозиториев

![image](screenshots/Screenshot_2.png)


`apt install apache2 -y` -  устанавливает веб-сервер Apache.

- `apt install` – команда для установки пакетов
- `apache2` – имя пакета Apache (веб-сервера)
- `-y` – флаг, который автоматически подтверждает установку

![image](screenshots/Screenshot_3.png)

`service apache2 start` - запускает службу Apache.

- `service` – утилита для управления системными сервисами.
- `apache2` – имя службы веб-сервера.
- `start` – команда для запуска сервиса.

![image](screenshots/Screenshot_4.png)

3. Открываю браузер и перехожу на страницу `http://localhost:8000/`. Вижу следующее: 

![image](screenshots/Screenshot_5.png)

Это стандартная страница Apache, оторая отображается при успешной установке и запуске веб-сервера. Это является подтверждением, что сервер работает корректно.

4. Выполняю следующие команды:

```bash
ls -l /var/www/html/
echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
```

`ls -l /var/www/html/`

- `ls` – команда для просмотра содержимого директории.
- `-l` – выводит подробную информацию о файлах (права доступа, владелец и тд).
- `/var/www/html/` – стандартная директория для размещения веб-страниц в Apache.

`echo '<h1>Hello, World!</h1>' > /var/www/html/index.html`

- `echo '<h1>Hello, World!</h1>` – выводит строку `<h1>Hello, World!</h1>`.
- `>` – перенаправляет этот вывод в файл, перезаписывая его (если файл уже существовал, его содержимое будет удалено).
- `/var/www/html/index.html` – файл, в который записывается строка

![image](screenshots/Screenshot_6.png)

Обновляю страницу и вижу:

![image](screenshots/Screenshot_7.png)

Я вижу то, что было введено в `index.html` прошлыми командами, а именно `echo <h1>Hello, World!</h1>`

5. Выполняю следующие команды:

```bash
cd /etc/apache2/sites-enabled/
cat 000-default.conf
```

- `cd /etc/apache2/sites-enabled/` - меняет директорию на указанную (папка, в которой хранятся конфигурационные файлы виртуальных хостов Apache.)
- `cat 000-default.conf` - выводит (командой `cat`) настройки основного виртуального хоста Apache (`000-default.conf` - конфигурационный файл виртуального хоста Apache, который отвечает за работу веб-сервера)

![image](screenshots/Screenshot_8.png)

Я вижу конфигурационный файл `Apache`, который определяет виртуальный хост, который обрабатывает HTTP-запросы на порт 80. Он устанавливает корневую директорию сайта `/var/www/html`, указывает email администратора `webmaster@localhost`, настраивает логирование `error.log и access.log`.

Закрываю окно командой `exit`.

![image](screenshots/Screenshot_9.png)

6. Просматриваю список текущих контейнеров

```bash
docker ps -a
```

Команда `docker ps -a` выводит список всех контейнеров в моей системе, включая активные, остановленные и завершившиеся. Флаг `-a` показывает полную информацию, такую как имена, ID, статус и т.д.

![image](screenshots/Screenshot_10.png)

Удаляю контейнер `containers04`

```bash
docker rm containers04
```

Команда `docker rm containers04` удаляет контейнер с именем `containers04`

![image](screenshots/Screenshot_11.png)


## Выводы
В ходе лабораторной работы я изучил основные команды `Debian/Ubuntu`, а также познакомился с `Docker` и его основными функциями. Я запустил контейнер с `Ubuntu`, установил веб-сервер `Apache` и успешно развернул простую веб-страницу с текстом `"Hello, World!"`.

## Библиография
1. Курс Контейнеризация и виртуализация [https://moodle.usm.md/mod/assign/view.php?id=282116](https://moodle.usm.md/mod/assign/view.php?id=282116)
2. Гайд по Apache [https://httpd.apache.org/docs/2.4/getting-started.html](https://httpd.apache.org/docs/2.4/getting-started.html)
3. Гайд по работе с Apache + Ubuntu [https://ubuntu.com/tutorials/install-and-configure-apache#1-overview](https://ubuntu.com/tutorials/install-and-configure-apache#1-overview)