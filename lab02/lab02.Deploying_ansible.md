LAB 2. Deploying Ansible. Solution.

1. Убедитесь, что пакет **ansible** установлен на узле управления, и запустите команду `ansible --version`.
   
2. В домашней директории пользователя student на **workstation**, **/home/student**, создайте новую директорию с именем **deploy-review**. Перейдите в эту директорию.
   
3. Создайте файл **ansible.cfg** в каталоге **deploy-review,** который вы будете использовать для установки следующих параметров Ansible по умолчанию:
- Подключайтесь к управляемым хостам как пользователь **devops**.
- Используйте подкаталог **inventory** для хранения файла **inventory**.
- Отключите повышение привилегий по умолчанию. Если повышение привилегий включено из командной строки, настройте параметры по умолчанию, чтобы Ansible использовал метод **sudo** для переключения на учетную запись пользователя **root**. Ansible не должен запрашивать пароль для входа в **devops** или пароль **sudo**

Управляемые хосты были настроены с использованием пользователя **devops**, который может входить в систему с использованием аутентификации на основе ключа SSH и может запускать любую команду от имени **root** с помощью команды **sudo** без пароля.

4. Создайте директорию **/home/student/deploy-review/inventory**.

Скачайте файл  http://materials.example.com/labs/deploy-review/inventory и сохраните его как статический файл inventory с именем **/home/student/deploy-review/inventory/inventory**.

5. Выполните команду **id** как ad hoc команду, предназначенную для группы **all** host, чтобы убедиться, что **devops** является удаленным пользователем и, что повышение привилегий по умолчанию отключено.
6. Выполните ad hoc команду, предназначенную для группы хостов **all**, которая использует модуль копирования для изменения содержимого файла **/etc/motd** на всех хостах. 

Используйте опцию **content** модуля **copy,** чтобы убедиться, что файл **/etc/motd** состоит из строки **This server is managed by Ansible. \n** в виде одной строки. (**\n**, используемый с параметром **content**, приводит к тому, что модуль помещает новую строку в конец строки.)

Вы должны запросить повышение привилегий из командной строки, чтобы заставить это работать с вашими текущими значениями по умолчанию **ansible.cfg**.

7. Если вы снова запустите ту же ad hoc команду, вы должны увидеть, что модуль **copy** определяет, что файлы уже являются правильными, и поэтому они не изменяются. Найдите ad hoc команду для сообщения **SUCCESS** и строку **"changed": false** для каждого управляемого хоста.
8. Чтобы подтвердить это другим способом, запустите ad hoc команду, предназначенную для группы хостов **all**, используя модуль command для выполнения команды `cat /etc/motd`. Выходные данные команды **ansible** должны отображать строку **This server is managed by Ansible.** для всех хостов. Вам не нужно повышение привилегий для этой специальной команды.