# CentOS 7 部署 DNS 服务器（BIND）

## 1. 安装 BIND 服务

```bash
sudo yum install bind bind-utils -y
```

---

## 2. 配置主文件

主配置文件路径：
```
/etc/named.conf
```

### 常见修改项：

- 修改监听地址（允许外部访问）：

```conf
listen-on port 53 { any; };
allow-query     { any; };
```

- 如果是公网 DNS，注释掉：
```conf
// listen-on-v6 port 53 { ::1; };
```

---

## 3. 配置区域文件（正向解析）

在 `/etc/named.rfc1912.zones` 中添加区域信息：

```conf
zone "example.com" IN {
    type master;
    file "/var/named/example.com.zone";
    allow-update { none; };
};
```

创建对应的区域数据文件：

```bash
sudo vim /var/named/example.com.zone
```

示例内容：

```dns
$TTL 86400
@   IN  SOA     ns1.example.com. admin.example.com. (
                2025042001 ; Serial
                3600       ; Refresh
                1800       ; Retry
                604800     ; Expire
                86400 )    ; Minimum TTL

    IN  NS      ns1.example.com.
ns1 IN  A       192.168.1.1
www IN  A       192.168.1.10
```

✅ 注意：BIND 区域文件必须以 `named` 用户可读写权限保存。

---

## 4. 配置反向解析（可选）

在 `/etc/named.rfc1912.zones` 中添加：

```conf
zone "1.168.192.in-addr.arpa" IN {
    type master;
    file "/var/named/192.168.1.zone";
};
```

文件 `/var/named/192.168.1.zone` 内容如下：

```dns
$TTL 86400
@   IN  SOA     ns1.example.com. admin.example.com. (
                2025042001 ; Serial
                3600       ; Refresh
                1800       ; Retry
                604800     ; Expire
                86400 )    ; Minimum TTL

    IN  NS      ns1.example.com.
1   IN  PTR     ns1.example.com.
10  IN  PTR     www.example.com.
```

---

## 5. 设置权限并检查语法

```bash
sudo chown named:named /var/named/*.zone
sudo named-checkconf
sudo named-checkzone example.com /var/named/example.com.zone
```

---

## 6. 启动并设置开机自启

```bash
sudo systemctl start named
sudo systemctl enable named
```

---

## 7. 防火墙配置

```bash
sudo firewall-cmd --permanent --add-service=dns
sudo firewall-cmd --reload
```

---

## 8. 客户端测试

### 临时指定 DNS 测试（适用于本机）：

```bash
dig @127.0.0.1 www.example.com
```

或：

```bash
nslookup www.example.com 127.0.0.1
```

---

## 9. 修改客户端 DNS 设置（永久）

编辑 `/etc/resolv.conf`：

```conf
nameserver 127.0.0.1
```

✅ 如果使用 NetworkManager，会自动覆盖该文件，建议通过配置 `nmcli` 或设置静态 DNS。

---

## 10. 常见问题与排查

| 问题                             | 可能原因                         | 解决方法                         |
|----------------------------------|----------------------------------|----------------------------------|
| DNS 无法访问                     | 防火墙未开放 53 端口             | `firewall-cmd` 放通 DNS 服务    |
| `SERVFAIL` 错误                  | 区域文件配置错误或权限问题       | 使用 `named-checkzone` 检查     |
| 客户端不能解析域名               | `/etc/resolv.conf` 设置不正确    | 添加 `nameserver` 指向 DNS 服务器 |
| SELinux 拒绝 DNS 文件访问       | SELinux 策略限制                 | 临时关闭：`setenforce 0`        |

---

## 常用命令汇总

```bash
# 检查配置语法
sudo named-checkconf

# 检查区域文件
sudo named-checkzone example.com /var/named/example.com.zone

# 查看 53 端口监听情况
sudo netstat -tulnp | grep named

# 关闭 SELinux（测试用）
sudo setenforce 0
```

---

## 目录结构总结

| 目的        | 路径                         |                |
| --------- | -------------------------- | -------------- |
| 主配置文件     | `/etc/named.conf`          |                |
| 区域配置文件    | `/etc/named.rfc1912.zones` |                |
| 正向/反向区域文件 | `/var/named/*.zone`        |                |
| 日志查看      | `/var/log/messages`        |                |
| 服务管理命令    | `systemctl [start          | status] named` |

---

## 小提示：正向与反向解析

- 正向解析：域名 → IP（最常用）
- 反向解析：IP → 域名（可选，但在邮件、日志系统中很有用）

