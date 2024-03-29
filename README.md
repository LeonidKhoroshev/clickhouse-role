Clickhouse
=========

Роль устанавливает и настраивает Clickhouse — колоночную СУБД, позволяющую выполнять аналитические запросы в режиме реального времени на структурированных больших данных. Роль включает в себя установку следующих пакетов:
- Clickhouse-server - содержит конфигурационные файлы для запуска Clickhouse в качестве сервера;
- Clickhouse-client - интерактивный консольный клиент;
- Сlickhouse-common-static - исполняемый файл Clickhouse.
 
Требования
------------

На настраиваемых хостах должна быть уствновлена ОС Linux (RPM линейка), так как установка производится пакетным менеджером yum. Для корректной работы playbook также требуется следующее ПО: Ansible - версия не ниже 2.10.
и Phyton - не ниже версии 3.6.


Переменные
--------------

Данная роль доступна к использованию без переменных, так как все значения прописаны в коде. При необходимости можно изменить отдельные настройки, такие как версия ПО (по умолчанию доступна версия "23.8.9.54"), имя пользователя, а также параметры создаваемой таблицы для хранения логов. 

Зависимости
--------------
Для обработки данных рекомендуется использовать Vector (роль доступна по [ссылке](https://github.com/LeonidKhoroshev/vector)) и графический интерфейc Lighthouse (роль доступна по [ссылке](https://github.com/LeonidKhoroshev/lighthouse) ). В сулчае, если базы данных, Vector и Lighthouse предполагается устанавливать на разных хостах, также потребуется веб-сервер (роль для установки Nginx доступна по [ссылке](https://github.com/LeonidKhoroshev/nginx)).

Пример плейбука
----------------

Установить роль можно через ansible-galaxy:
```
ansible-galaxy install -r requirements.yml
```

указав в файле requirements.yml cледующее содержание:
```
  - src: https://github.com/LeonidKhoroshev/clickhouse-role
    scm: git
    name: clickhouse-role
```

Далее вписываем роль в плейбук:
```
- name: Install Clickhouse
  hosts: clichouse
  remote_user: leo
  become: true
  roles:
    - clickhouse-role
```
