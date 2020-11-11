# Vagrantfile - создание одной виртуалки Centos 7

Провизион - ansible - устанавливает nginx c роли nginx)

nginx

defaulst/main.yml        - переменные по умолчанию
tasks/
   main.yml,             - главный таск
   setup-RedHat.yml,     - установка nginx под RedHat
   vhosts.yml            - установка vhosts

vars/RedHat.yml          - переменные под RedHat
templates/
   nginx.conf.j2         - шаблон j2 конфиг nginx
   nginx.repo.j2         - шаблон j2 repo nginx
   vhost.j2              - шаблон j2 vhost

handlers/main.yml        - перезапуск nginx 





