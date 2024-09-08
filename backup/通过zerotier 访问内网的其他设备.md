> [!note]
> zerotier安装完成后如何访问内网的其他设备呢？
> 有些设备并不支持安装又如何解决呢？
> 这就是这个文章记录的我的折腾内容。
### 开启端口转发
```shell
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
sysctl -p
```
> 如果回显 net.ipv4.ip _forward = =1 则表示开启成功


### iptables 设置

 - iptables 端口转发
 
```shell
iptables -A FORWARD -i zt3jn72ets -j ACCEPT
iptables -A FORWARD -o zt3jn72ets -j ACCEPT
iptables -t nat -A POSTROUTING  ! -o lo -j MASQUERADE
```
>[!important]
>这里zt3jn72ets为zerotier虚拟网卡在不同的机器中不一样，你可以在路由器ssh环境中用 zerotier-cli listnetworks 或者 ifconfig 查询zt开头的网卡名 。
- 用 iptables-persistent保存规则防止重启失效
  - 安装iptables-persistent
```shell
apt-get install iptables-persistent
```
- 保存规则
```shell
sh -c "iptables-save > /etc/iptables/rules.v4"
```

