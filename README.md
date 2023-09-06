# Linux_Lesson_26
## Backups

### Описание репозитория

Лабораторный стенд для удаленного резервного копирования каталога /etc c клиентского хоста на сервер с установленным borgbackup, настраиваемые с использованием Vagrant и Ansible. Все файлы и структуру директории temрlates необходимо скопировать в общую директорию.  

**Vagrantfile** - создает две виртуальные машины: сервер и клиент. К серверу подключен дополнительный носитель емкостью 2 Гб. Настройка функциональности хостов производится с помощью Ansible.

> [!IMPORTANT]
> Для использования дополнительного жесткого диска в Vagrant необходимо ввести команду: 

	export VAGRANT_EXPERIMENTAL="disks"

**hosts** - файл с настройками компьютеров для быстрого доступа к ним из playbook.  
**main.yml** - основной файл Ansible playbook для установки и настройки сервера хранения резервных копий и клиентского хоста (все шаги описаны в файле).  
Директория **/templates** содержит файлы для копирования на клиентский хост необходимых сервисов для управления резервным копированием.

> [!IMPORTANT]
> После установки и настройки виртуальных машин с помощью Ansible необходимо инициализировать репозиторий borg на сервере резервирования, войдя на клиентский хост ввести команду и установить парольную фразу "111":

  	borg init --encryption=repokey borg@192.168.56.10:/var/backup/
Для использования отличной от "111" парольной фразы необходимо изменить значение Environment="BORG_PASSPHRASE=111" в файле templates/borg-backup.service

---

### Проверка работоспособности стенда

Список резервных копий на сервере
![borg_files](https://github.com/darknetworm/Linux_Lesson_26/assets/82410807/a1f3e482-fcf4-480f-81cc-56358e309628)
Логи выполнения резервного копирования
![syslog](https://github.com/darknetworm/Linux_Lesson_26/assets/82410807/d785a175-fc0a-4838-9eee-faf3efde6e54)
**borg_restore.txt** - файл процесса восстановления из резервной копии, записанный утилитой scrupt

