# 一些杂物
# 封锁censys、shodan 扫描IP
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
