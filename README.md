# 一些杂物
# 封锁censys、shodan 扫描IP iptables已经允许端口访问, 再执行这脚本就没啥效果了，需要在开放端口之前drop掉 这些 IP
```Bash
wget https://raw.githubusercontent.com/smlemk3/mytools/main/block_censys_shodan.sh && chmod +x block_censys_shodan.sh
```

# 新debian 11 12 /etc/rc.local 开机启动
```Bash
cat <<EOF >/etc/rc.local
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

exit 0
EOF
```
```Bash
chmod +x /etc/rc.local && systemctl enable --now rc-local
#可能会出现警告信息，无视
```
# moeclub 网络安装debian脚本
```Bash
bash <(wget --no-check-certificate -qO- 'https://raw.githubusercontent.com/MoeClub/Note/master/InstallNET.sh') -d 12 -v 64 -p "younewpass" -port 8222
```

