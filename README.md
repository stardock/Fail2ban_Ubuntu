# Fail2ban_Ubuntu
Fail2ban for ubuntu

$ sudo vi /etc/fail2ban/jail.local  

```
[DEFAULT]
# 以空格分隔的列表，可以是 IP 地址、CIDR 前缀或者 DNS 主机名
# 用于指定哪些地址可以忽略 fail2ban 防御
ignoreip = 127.0.0.1 172.31.0.0/24 10.10.0.0/24 192.168.0.0/24

# 客户端主机被禁止的时长（秒）
bantime = 864000

# 客户端主机被禁止前允许失败的次数 
maxretry = 10

# 查找失败次数的时长（秒）
findtime = 7200

mta = sendmail

[ssh-iptables]
enabled = true
filter = sshd
action = iptables[name=SSH, port=ssh, protocol=tcp]
sendmail-whois[name=SSH, dest=your@email.com, sender=fail2ban@email.com]
# Debian 系的发行版 
logpath = /var/log/auth.log
# Red Hat 系的发行版
logpath = /var/log/secure
# ssh 服务的最大尝试次数 
maxretry = 10
```

Reference:  
https://www.linuxprobe.com/fail2ban-ssh-crack.html
