## Описание playbook для настройки виртуальных машин Yandex Cloud"
В каталоге playbook/inventory расположены каталоги, имена которых соответствуют средам и указываются в качестве параметра -i при запуске playbook

Каталог playbook/inventory/prod содержит описание среды prod.

В каталоге playbook/inventory/prod расположен каталог group_vars, в котором содержится описание переменных для среды prod.

В каталоге playbook/inventory/prod расположен файл hosts.yml, в котором описаны хосты, к которым будет применен playbook.

В каталоге playbook/template распложены jinja-файлы шаблонов для настройки разворачиваемых сервисов в процессе выполнения playbook.

Файл playbook/site.yml - playbook.

Playbook состоит из 3 play:
1. Установка Elasticsearch:
   1. происходит определения списка хостов к которым будет применен play, в данном случае - elasticsearch
   2. описание handler по рестату сервиса elasticsearch
   3. описание задач по установке elasticsearch:
      1. происхолдит скачивание rmp файла Elasticsearch версии, указанной в файле playbook/inventory/group_vars/elasticsearch.yml, с официального сайта на хост elasticsearch в каталог /tmp
      2. происходит установка elasticsearch из скачанного rmp файла
      3. происходит генерация файла конфигурации elasticsearch из файла шаблона, задание данному файлу прав, вызов handler для рестарта elasticsearch

2. Установка Kibana:
   1. происходит определения списка хостов к которым будет применен play, в данном случае - kibana
   2. описание handler по рестату сервиса kibana
   3. описание задач по установке kibana:
      1. происхолдит скачивание rmp файла kibana версии, указанной в файле playbook/inventory/group_vars/kibana.yml, с официального сайта на хост kibana в каталог /tmp
      2. происходит установка kibana из скачанного rmp файла
      3. происходит генерация файла конфигурации kibana из файла шаблона, задание данному файлу прав, вызов handler для рестарта kibana

3. Установка Filebeat:
   1. происходит определения списка хостов к которым будет применен play, в данном случае - filebeat
   2. описание handler по рестату сервиса filebeat
   3. описание задач по установке filebeat:
      1. происхолдит скачивание rmp файла filebeat версии, указанной в файле playbook/inventory/group_vars/filebeat.yml, с официального сайта на хост filebeat в каталог /tmp
      2. происходит установка filebeat из скачанного rmp файла
      3. происходит генерация файла конфигурации filebeat из файла шаблона, задание данному файлу прав, вызов handler для рестарта filebeat
      4. подключение модуля system для работы filebeat
      5. запуск процесса инициализации dashbord в kibana послу установки filebeat

##вывод ansible-lint site.yml
![](img/ans-lint.png)
