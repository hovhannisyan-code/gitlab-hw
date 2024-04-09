# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Оганесян Гор`

### Задание 1

`Установите Zabbix Server с веб-интерфейсом.`

1. `Прикрепите в файл README.md скриншот авторизации в админке.`
2. `Приложите в файл README.md текст использованных команд в GitHub`

Скриншоты
![Zabbix Frontend Login](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_0.png)
![Zabbix Frontend Dashboard](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_1.png)

```
# Установка PostgreSQL
sudo apt install postgresql

# Установка Zabbix Server, веб-интерфейс
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-nginx-conf zabbix-sql-scripts

# Создание базы данных и пользователя PostgreSQL для Zabbix
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD
'\'123456789\'';"'
su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'

# Импорт схемы и начальных данных в базу данных PostgreSQL
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# Настройка Zabbix Server
sed -i 's/# DBPassword=/DBPassword=123456789/g' /etc/zabbix/zabbix_server.conf

# Настройка PHP для веб-интерфейса
sudo nano /etc/zabbix/nginx.conf
listen 8080;
server_name example.com;

# Перезапуск Zabbix Server, Nginx, php-fpm
systemctl restart zabbix-server nginx php8.1-fpm
systemctl enable zabbix-server nginx php8.1-fpm
```

---

### Задание 2

`Установите Zabbix Agent на два хоста.`

1. `Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу`
2. `Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером`
3. `Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.`
4. `Приложите в файл README.md текст использованных команд в GitHub`

Скриншоты
![Hosts](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_2.png)
![Logs](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_3.png)
![Latest Data](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_4.png)

```
Поле для вставки кода...
# Установка Zabbix агент
apt install zabbix-agent
sed -i 's/Server=127.0.0.1/Server=YOUR IP ADDRESS'/g' /etc/zabbix/zabbix_server.conf
systemctl restart zabbix-agent
systemctl enable zabbix-agent

```

### Задание 3 со звёздочкой\*

`Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.`

1. `Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:`

Скриншоты

![Free Space](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_5.png)
![Item](https://github.com/hovhannisyan-code/gitlab-hw/blob/main/img/Screenshot_6.png)
