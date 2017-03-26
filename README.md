# Docker image of i-doit - CMDB and IT documentation.
This image is based on the MODIUS-TECHBLOG howto article http://www.modius-techblog.de/linux/doit-richtig-unter-ubuntu-16-04-xenial-xerus-installieren/ .

> i-doit documents your IT-infrastructure. From cables to servers, from software to licences, any component with a plug or running software is worth being documented. And what’s better than having a central platform for it? The scope is defined by you – whether it’s just IP-addresses, accounting information or complex technical details – i-doit fulfills all your documentation needs.
> https://www.i-doit.org/

## Enable dedicated MySQL server?
If you want to install a dedicated MySQL server inside the container you will have to uncomment the following lines.

### Dockerfile
```sh
# install mysql 5.6
# Uncomment the following line if you want to install mysql inside the container.
RUN apt-get update && apt-get install -y -q mysql-server-5.6

# configure mysql 5.6 for i-doit 1.8
# Uncomment the following line if you want to install mysql inside the container.
COPY mysql-for-i-doit-1-8.cnf /etc/mysql/conf.d
```

### supervisord.conf
```sh
; Uncomment the following lines if you want to install mysql inside the container.
[program:mysqld]
command=/usr/sbin/mysqld --basedir=/usr --datadir=/var/lib/mysql --user=mysql --pid-file=/var/run/mysqld/mysqld.pid --skip-external-locking --port=3306 --socket=/var/run;/mysqld/mysqld.sock
```

