# CentOS 7 配置 DHCP 服务器

---

## 1. 安装 DHCP 服务

```bash
sudo yum install dhcp -y
```

---

## 2. 主配置文件路径

```
/etc/dhcp/dhcpd.conf
```

---

## 3. 编辑 DHCP 配置文件

```bash
sudo vim /etc/dhcp/dhcpd.conf
```

### 示例配置：

```conf
# 全局设置
default-lease-time 600;
max-lease-time 7200;
authoritative;

# 子网设置
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;     # 可分配IP范围
    option routers 192.168.1.1;            # 默认网关
    option subnet-mask 255.255.255.0;
    option domain-name-servers 8.8.8.8, 114.114.114.114;
    option domain-name "localdomain";
}
```

### 指定静态 IP（可选）：

```conf
host printer {
    hardware ethernet 00:11:22:33:44:55;
    fixed-address 192.168.1.250;
}
```

---

## 4. 启用并启动 DHCP 服务

```bash
sudo systemctl start dhcpd
sudo systemctl enable dhcpd
```

✅ 启动成功后，服务将监听 `UDP 67` 端口，向局域网客户端分配 IP。

---

## 5. 配置防火墙

```bash
sudo firewall-cmd --permanent --add-service=dhcp
sudo firewall-cmd --reload
```

---

## 6. 验证配置是否正确

```bash
sudo dhcpd -t
```

✅ 返回空说明配置无误。

---

## 7. 客户端测试获取 IP

在客户端执行：

```bash
dhclient -v
```

或重新连接网络，查看是否获取到 DHCP 分配的 IP。

---

## 8. 日志查看与排错

```bash
tail -f /var/log/messages
```

常见日志关键字：`DHCPDISCOVER`、`DHCPOFFER`、`DHCPREQUEST`、`DHCPACK`。

---

## 9. 常见问题与解决

| 问题                            | 可能原因                       | 解决方案                         |
|---------------------------------|--------------------------------|----------------------------------|
| 客户端未获取 IP                | 配置文件有误                  | 用 `dhcpd -t` 检查语法            |
| 客户端请求未到达服务器         | 防火墙或网段隔离              | 检查物理连接、防火墙设置         |
| 服务未监听端口                 | 服务未启动或报错              | `systemctl status dhcpd` 查看状态 |
| 日志提示权限或文件错误         | 区域权限或目录错误            | 确保 `/etc/dhcp` 可访问          |

---

## 10. DHCP 配置文件结构小结

| 功能             | 语句                             |
|------------------|----------------------------------|
| 默认租约时间     | `default-lease-time`             |
| 最大租约时间     | `max-lease-time`                 |
| 声明为主 DHCP    | `authoritative`                  |
| 子网声明         | `subnet`                         |
| 地址池范围       | `range`                          |
| 默认网关         | `option routers`                 |
| DNS 服务器       | `option domain-name-servers`     |
| 域名             | `option domain-name`             |
| 静态绑定         | `host` + `hardware ethernet`     |

---

## 附：DHCP 相关服务命令

```bash
# 启动服务
sudo systemctl start dhcpd

# 设置开机自启
sudo systemctl enable dhcpd

# 查看状态
sudo systemctl status dhcpd

# 检查配置文件语法
sudo dhcpd -t

# 日志查看
tail -n 50 /var/log/messages
```
