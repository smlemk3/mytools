# debian12 安装mariadb10.4.x
```bash
apt install libaio-dev libncurses5 -y
wget https://mirrors.xtom.jp/mariadb/mariadb-10.4.33/bintar-linux-systemd-x86_64/mariadb-10.4.33-linux-systemd-x86_64.tar.gz
groupadd mysql
useradd -g mysql mysql

groupadd mysql
useradd -s /sbin/nologin -M -g mysql mysql

mkdir -p /data/db
chown -R mysql:mysql /data/db
tar zxvf mariadb-10.4.32-linux-systemd-x86_64.tar.gz
mv mariadb-10.4.32-linux-systemd-x86_64 /usr/local/mysql
chown -R mysql:mysql /usr/local/mysql
cp /usr/local/mysql/support-files/wsrep.cnf  /etc/my.cnf
echo basedir=/usr/local/mysql >> /etc/my.cnf
echo datadir=/data/db >> /etc/my.cnf

/usr/local/mysql/scripts/mysql_install_db --datadir=/data/db/ --basedir=/usr/local/mysql --defaults-file=/etc/my.cnf --user=mysql
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
chmod 755 /etc/init.d/mysql
cp /usr/local/mysql/support-files/systemd/mariadb.service /usr/lib/systemd/system/mariadb.service

sed -i 's/-\/usr\/local\/mysql\/data/\/data\/db/g' /usr/lib/systemd/system/mariadb.service

systemctl start mariadb.service
systemctl enable mariadb.service

echo 'export PATH=$PATH:/usr/local/mysql/bin/' >> ~/.bashrc
source ~/.bashrc
```
# mysql 安全设置
```bash
/usr/local/mysql/bin/mysql_secure_installation
```
# iptables 设置
```bash
apt install -y iptables-persistent
iptables -I INPUT 1 -i lo -j ACCEPT
iptables -I INPUT 2 -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -I INPUT 3 -p tcp --dport 22 -j ACCEPT
iptables -I INPUT 3 -p tcp --dport 65522 -j ACCEPT
iptables -I INPUT 4 -p tcp --dport 80 -j ACCEPT
iptables -I INPUT 5 -p tcp --dport 443 -j ACCEPT
iptables -I INPUT 6 -p tcp --dport 3306 -j DROP
iptables -I INPUT 7 -p icmp -m icmp --icmp-type 8 -j ACCEPT
#禁止所有入栈
#iptables -P INPUT DROP
/etc/init.d/netfilter-persistent save
/etc/init.d/netfilter-persistent reload
```
