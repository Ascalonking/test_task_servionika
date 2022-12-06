# test_task_servionika


 # Выполнение тестового задания № 1

 - [X] Задание 1.1
 - [ ] Задание 1.2 (усложненное)

 ## Задание:
 • Установить VirtualBox (или VMware workstation player), разобраться как  создать виртуальную машину и создать новую vm на базе дистрибутива  Centos  ( Centos это параллельная open source ветка rhel );
 
 • Подключиться к созданной vm по ssh через любой клиент.;
 
 • Установить Python на созданной vm;
 
 • В домашней директорий пользователя создать папку task; реализовать собственное key-values хранилище на Python. Данные будут сохраняться в файле storage.data(в формате JSON, можно использовать библиотеку tempfile, для хранения данных во временных файлах). Добавление новых данных в хранилище и получение текущих значений осуществляется с помощью утилиты командной строки storage.py. Пример работы утилиты:  
 
 Сохранение данных
 
 $ storage.py --key key_name --val value
 
 Получение данных
 
 $ storage.py --key key_name
 
 Обратите внимание, что значения по одному ключу не перезаписываются, а добавляются к уже сохраненным. Другими словами - по одному ключу могут храниться несколько значений. При выводе на печать, значения выводятся в порядке их добавления в хранилище (Пример ввода "test_value,test_value2,test_value3" ). Формат вывода на печать для нескольких значений через запятую. Если значений по ключу не было найдено, выведите пустую строку или None. Сделать обработку исключений, если они будут возникать при тестировании. Скрипт должен работать в разных ОС

 ## В процессе сделано:

 1. На систему виртуализации (VirtualBox), была создана новая vm на базе дистрибутива  CentOS7;
 2. Подключился к созданной vm по ssh с помощью SuperPuTTY.;
 3. Установил Python на созданной vm;
 4. В домашней директорий пользователя создал директорию task;
 5. В директории был создан файл storage.py для реализации собственного key-values хранилище на Python


 ## Как запустить проект:
  - $ python3 storage.py --key key_name --val value1
  - $ python3 storage.py --key key_name --val value2
  - $ python3 storage.py --key key_name --val value3

 ## Как проверить работоспособность:
 - Вывод  value1, value2, value3

 ## PR checklist
 - [X] Выставил label с темой тестового задания

# Выполнение тестового задания № 2

 - [X] Задание 2.1
 - [ ] Задание 2.2 (усложненное)

## Задание:
Создать 2 WEB сервера с выводом страницы «Hello Word! \n Server 1» (аналогично для второго Server 2). Сделать балансировку нагрузки (HA + keepalived), чтобы при обновлении страницы мы попадали на любой из WEB серверов(Для балансировки можно сделать 2 отдельных сервера, в сумме 4).
Будет плюсом использование Docker.

## В процессе сделано:

 1. На систему виртуализации (VirtualBox), были созданы 6 vm на базе дистрибутивов 2 Web Servers (Ubuntu 20.04), 2 Proxy servers (Ubuntu 20.04) и 2 routers (RouterOS 7);
 2. На вм машшинах RouterOS поднял сеть и настроил vrrp. команды по настрйоке находятс в '''Router 1''' и '''Router 2'''
    - Roter 1 ip addres 192.168.1.76 (Master)
    - Roter 2 ip addres 192.168.1.77 (Backup)
    - Virtual IP 192.168.1.78
 3. На вм машшинах Web Servers (Ubuntu 20.04) были установлены web сайт на nginx в docker, с выводом страницы «Hello Word! Server 1» (аналогично для второго Server 2), перед запуском docker контейнера создал HTML-страницу index.html, команды по настрйоке и запуску docker находятся в файле DockerNginx_run  
    - Запуск докер конейнера docker run -it --rm -d -p 8080:80 --name web -v ~/site-content:/usr/share/nginx/html nginx
    - Web 1 ip address 192.168.1.81
    - Web 2 ip address 192.168.1.82
 4. На вм машшинах HAProxy + keepalived (Ubuntu 20.04), команды по настрйоке HAProxy находятс в файле HAProxy файл конфигрурации haproxy.cfg находится в Proxy 1_haproxy.cfg и Proxy 2_haproxy.cfg файл конфигрурации keepalived.conf находятс в Proxy1_keepalived.conf и Proxy2_keepalived.conf
    - HAProxy 1 ip addres 192.168.1.79 (Master)
    - HAProxy 2 ip addres 192.168.1.80 (Backup)
    - Virtual IP 192.168.1.100

 ## Как проверить работоспособность:
 - Для проверки работоспособности web сервера 1 перейдите по url в браузере 192.168.1.81:8080
    - должно отобразиться надпись Hello world from Nginx container! SERVER 1

 - Для проверки работоспособности web сервера 2 перейдите по url в браузере 192.168.1.82:8080
    - должно отобразиться надпись Hello world from Nginx container! SERVER 2

 - Для проверки работоспособности HAProxy 1 перейдите по url в браузере http://192.168.1.79/haproxy?stats

 - Для проверки работоспособности HAProxy 1 перейдите по url в браузере http://192.168.1.80/haproxy?stats

 - Для проверки работоспособности keepalived перейдите по url в браузере 192.168.1.100
   - должно отобразиться надпись Hello world from Nginx container! SERVER 1
   - обновить страницу должно отобразиться надпись Hello world from Nginx container! SERVER 2
 
 ## Схема сети:
 ![screenshot](https://github.com/Ascalonking/test_task_servionika/blob/main/task_2/network%20diagram.png)
 
 ## PR checklist
 - [X] Выставил label с темой тестового задания