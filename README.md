# Домашнее задание к занятию "`Резервное копирование баз данных`" - `Макаров Денис`


### Инструкция по выполнению домашнего задания
<details>
   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)
</details>


### Задание 1. Резервное копирование

### Кейс
Финансовая компания решила увеличить надёжность работы баз данных и их резервного копирования. 

Необходимо описать, какие варианты резервного копирования подходят в случаях: 

1.1. Необходимо восстанавливать данные в полном объёме за предыдущий день.

1.2. Необходимо восстанавливать данные за час до предполагаемой поломки.

1.3.* Возможен ли кейс, когда при поломке базы происходило моментальное переключение на работающую или починенную базу данных.

### Ответ:

1.1 В данном случае я бы делал полный бэкап раз в неделю. Потом каждый день дифференциальный бэкап, который охватывает все изменения с момента последнего бэкапа.

1.2 Тут тоже для начала полный бэкап, но желательно раз в день. И потом в течение дня инкрементный, т.к. по занимаемой памяти и времени он будет самый экономный.

1.3 Кейс master-slave

---

### Задание 2. PostgreSQL

2.1. С помощью официальной документации приведите пример команды резервирования данных и восстановления БД (pgdump/pgrestore).

### Ответ:

2.1 Базовая команда `pg_dump <имя_базы> > <файл_сохранения>`.

Команда `pg_restore`  извлекает архивный файл, созданный командой `pg_dump`, и восстанавливает выбранную базу данных PostgreSQL. Для указания базы данных нужно задать параметр `-d` - `pg_restore <имя_базы> <файл_сохранения>`.

---

### Задание 3. MySQL

3.1. С помощью официальной документации приведите пример команды инкрементного резервного копирования базы данных MySQL. 

### Ответ: 

Для данного вида резеревирования используется команда `mysqlbackup` с параметром `--incremental-base=history:last_full_backup`.

Также можно использовать и сторонние утилиты. Например, Percona XtraBackup, которая позволяет делать архивы баз данных на лету без блокировок таблиц. Например, `xtrabackup --backup --target-dir=/backupdb/inc1 --incremental-basedir=/backupdb/full`.

---


