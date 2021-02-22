# otus-linux
Vagrantfile - для стенда урока 9 - Network

# Дано
Vagrantfile с начальным  построением сети
inetRouter
centralRouter
centralServer

тестировалось на virtualbox

# Планируемая архитектура
построить следующую архитектуру

Сеть office1
- 192.168.2.0/26      - dev
- 192.168.2.64/26    - test servers
- 192.168.2.128/26  - managers
- 192.168.2.192/26  - office hardware

Сеть office2
- 192.168.1.0/25      - dev
- 192.168.1.128/26  - test servers
- 192.168.1.192/26  - office hardware


Сеть central
- 192.168.0.0/28    - directors
- 192.168.0.32/28  - office hardware
- 192.168.0.64/26  - wifi

```
Office1 ---\
      -----> Central --IRouter --> internet
Office2----/
```
Итого должны получится следующие сервера
- inetRouter
- centralRouter
- office1Router
- office2Router
- centralServer
- office1Server
- office2Server

# Теоретическая часть
- Найти свободные подсети
- Посчитать сколько узлов в каждой подсети, включая свободные
- Указать broadcast адрес для каждой подсети
- проверить нет ли ошибок при разбиении

# Практическая часть
- Соединить офисы в сеть согласно схеме и настроить роутинг
- Все сервера и роутеры должны ходить в инет черз inetRouter
- Все сервера должны видеть друг друга
- у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи
- при нехватке сетевых интервейсов добавить по несколько адресов на интерфейс

# Проверка Выполненой работы
- Для проверки надо скачать репозиторий 

      cd ~
      git clone git@github.com:Timurka4080/otus-linux.git

- Затем надо перейти в ветку __network__

      git checkout network

- Далее надо запусть vm при помощи vagrant и Amsible для настройки топологоии

      cd otus-linux
      vagrant up 
      ansible-playbook playbook.yml

![Топология](Topo1.pdf) 

- Выше указана подробная топология которая получается в результате. Но есть какие-то проблемы либо у меня на локальной машине или это у Ansible. Так как на все машинах которые выступают в роли Router нажно отдельно выполнить две команды 

      sysctl net.ipv4.conf.all.forwarding=1
      systemctl restart network

- На машинах выполняющих роль Server надо выполнить только перезагрузку сетевого демона.

      systemctl restart network

- По какой причине эти команды не срабатываю в provision эти команды я так и не нашел. 




