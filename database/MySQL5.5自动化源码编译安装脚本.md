# MySQL5.5自动化源码编译安装脚本

最近，闲着没事，就写了一个简单的自动化安装脚本。
环境： `RHEL5.5`
源码包和安装脚本需要放在同一级目录，如下所示：
```
[root@rhel5 mysql5.5-install]# ls -lh
total 29M
-rw-r--r--. 1 root root 5.5M May  3 15:05 cmake-2.8.8.tar.gz
-rw-r--r--. 1 root root  23M May  3 20:36 mysql-5.5.13.tar.gz
-rwxr-xr-x. 1 root root 2.0K May  4 14:49 mysql5.5-install.sh
```


下面是`mysql5.5-install.sh`脚本的源码：
```bash
#!/bin/bash
# Filename: mysql5.5-install.sh 
# Lok cjinle@gmail.com 2012/05/04

# variable PATH
BASE_DIR=$(dirname -- $(readlink -f -- "$0"))
MYSQL_BASE_DIR=/usr/local/mysql
MYSQL_LOG_DIR=/var/log/mysqld
MYSQL_PID_DIR=/var/run/mysqld
MYSQL_SOCKET_DIR=/tmp


# check cmake whether installed
which cmake > /dev/null 2>&1
ret=$?
if [ "$ret" -ne "0" ]; then
    echo "cmake is not installed!"
    tar xvf ${BASE_DIR}/cmake-2.8.8.tar.gz -C /usr/src/
    cd /usr/src/cmake-2.8.8
    ./bootstrap && gmake && make install
fi

# install mysql-5.5.13
if [ -e "$MYSQL_BASE_DIR" ]; then
    echo "old mysql dir exist"
else
    tar xvf ${BASE_DIR}/mysql-5.5.13.tar.gz -C /usr/src/
    cd /usr/src/mysql-5.5.13
    cmake . -DCMAKE_INSTALL_PREFIX=${MYSQL_BASE_DIR} -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci -DWITH_EXTRA_CHARSETS=utf8,gbk,gb2312 -DENABLED_LOCAL_INFILE=1 -DWITH_INNOBASE_STORAGE_ENGINE=1 -DWITH_ARCHIVE_STORAGE_ENGINE=1 -DWITH_PARTITION_STORAGE_ENGINE=1
    gmake && make install
fi

id mysql > /dev/null 2>&1
ret=$?
if [ "$ret" -ne "0" ]; then
    useradd mysql
fi

[ -e "$MYSQL_LOG_DIR" ] || mkdir -p "$MYSQL_LOG_DIR"
chown mysql:mysql $MYSQL_LOG_DIR

[ -e "$MYSQL_PID_DIR" ] || mkdir -p "$MYSQL_PID_DIR"
chown mysql:mysql $MYSQL_PID_DIR

[ -e "${MYSQL_BASE_DIR}/etc" ] || mkdir "${MYSQL_BASE_DIR}/etc"
cat > ${MYSQL_BASE_DIR}/etc/my.cnf <<EOF
[mysqld]
port=3306
pid-file=${MYSQL_PID_DIR}/mysqld.pid
socket=${MYSQL_SOCKET_DIR}/mysqld.socket
log=${MYSQL_LOG_DIR}/mysqld.log
log-error=${MYSQL_LOG_DIR}/mysqld-err.log

[client]
socket=${MYSQL_SOCKET_DIR}/mysqld.socket
EOF

cd $MYSQL_BASE_DIR

# init mysql database
${MYSQL_BASE_DIR}/scripts/mysql_install_db --defaults-file=${MYSQL_BASE_DIR}/etc/my.cnf --user=mysql --basedir=${MYSQL_BASE_DIR}

ret=$?
[ "$ret" -eq "0" ] && echo "init mysql basebase success" || exit 1

read -p "start mysql now [Y/N]: " start_flg

if [ "$start_flg" = "Y" ]; then
    ${MYSQL_BASE_DIR}/bin/mysqld_safe --defaults-file=${MYSQL_BASE_DIR}/etc/my.cnf --user=mysql &
else
    exit 1
fi
```