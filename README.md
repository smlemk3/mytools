# 一些杂物
Debian iptables 配置
[Debian_iptables_setting.md](https://github.com/smlemk3/mytools/blob/main/Debian_iptables_setting.md)

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

