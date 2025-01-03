# ipv6
vps生成ipv6地址

### Ubuntu 18.04 及更高版本 ###
1. 编辑 Netplan 配置文件：
sudo vi /etc/netplan/01-netcfg.yaml

2. 找到对应的网络接口，添加 IPv6 地址。例如：
```
network:
  version: 2
  ethernets:
    enp1s0:
      addresses:
        - 2001:19f0:4400:64f1:72ea:1da6:6c34:5a88/128
        - 2001:19f0:4400:64f1:49da:0861:27b6:31cf/128
        - 2001:19f0:4400:64f1:7a39:0194:4103:5f64/128
        - 2001:19f0:4400:64f1:6d13:3b58:114f:28a3/128
```

4. 应用配置：
sudo netplan apply

### Debian和较旧的 Ubuntu 版本 ###
1. 编辑 /etc/network/interfaces 文件：
sudo vi /etc/network/interfaces
或者 进入 /etc/network/interfaces.d/
新建文件 ipv6

3. 添加或修改相关接口的配置：
```
auto enp1s0
iface enp1s0 inet6 static
    address 2001:19f0:4400:64f1:5400:5ff:fe09:2df1/64 
    up /sbin/ip -6 addr add 2001:19f0:4400:64f1:524c:1be0:5f94:3a18/128 dev enp1s0
```

4. 重启网络服务
sudo systemctl restart networking
