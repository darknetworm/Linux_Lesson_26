# Linux_Lesson_26
## Backups
---
Описание репозитория

Лабораторный стенд для удаленного резервного копирования каталога /etc c клиентского хоста на сервер с настроенным borgbackup, настраиваемые с использованием Vagrant и Ansible. Все файлы и структуру директорий temрlates необходимо скопировать в одну директорию.

Vagrantfile - создает две виртуальные машины: сервер и клиент. К серверу подключен дополнительный носитель емкостью 2 Гб. Настройка функциональности хостов производится с помощью Ansible.

> [!IMPORTANT]
> Для использования дополнительного жесткого диска в Vagrant необходимо ввести команду: 

	export VAGRANT_EXPERIMENTAL="disks"

hosts - файл с настройками компьютеров для быстрого доступа к ним из playbook.

main.yml - основной файл Ansible playbook для установки и настройки сервера хранения резервных копий и клиентского хоста (все шаги описаны в файле).

Директория /templates содержит файлы для копирования на клиентский хост необходимых сервисов для управления резервным копированием.

> [!IMPORTANT]
> После установки и настройки виртуальных машин с помощью Ansible необходимо инициализировать репозиторий borg на сервере резервирования войдя на клиентский хост и введя команду:

  	borg init --encryption=repokey borg@192.168.56.10:/var/backup/

---
