# CentOS 7 部署 Web 服务器（Apache）

## 1. 安装 Apache（httpd）

```bash
sudo yum install httpd -y
```

---

## 2. 启动 Apache 服务并设置开机自启

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

## 3. 配置防火墙允许 HTTP/HTTPS

```bash
# 开放 HTTP 和 HTTPS 服务端口
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

📝 如果不确定是否已开启防火墙，可以关闭防火墙进行测试：
```bash
sudo systemctl stop firewalld
sudo systemctl disable firewalld
```

---

## 4. 默认站点目录说明

- 默认网页根目录：
  ```
  /var/www/html
  ```
  把网页文件（如 `index.html`）放入此目录即可被访问。

- 示例创建网页文件：
  ```bash
  echo "Hello from Apache on CentOS 7" | sudo tee /var/www/html/index.html
  ```

---

## 5. 主要配置文件及目录说明

| 项目        | 路径                          | 说明                           |
|-------------|-------------------------------|--------------------------------|
| 主配置文件  | `/etc/httpd/conf/httpd.conf`  | Apache 的核心配置              |
| 配置目录    | `/etc/httpd/conf.d/`          | 可放置虚拟主机、自定义配置文件 |
| 日志目录    | `/var/log/httpd/`             | 存放访问日志、错误日志         |
| 默认网站目录| `/var/www/html/`              | 站点根目录                     |
| 服务控制    | `systemctl [start|stop|restart] httpd` | 控制 Apache 服务 |

---

## 6. 测试访问

### 通过浏览器或 curl 测试
```bash
curl http://localhost
```

输出应为你放在 `/var/www/html/index.html` 中的内容。

---

## 7. 虚拟主机配置（可选）

在 `/etc/httpd/conf.d/` 中创建配置文件：

```bash
sudo vim /etc/httpd/conf.d/mysite.conf
```

添加内容：

```apache
<VirtualHost *:80>
    ServerName www.mysite.com
    DocumentRoot /var/www/mysite
    ErrorLog logs/mysite-error.log
    CustomLog logs/mysite-access.log combined
</VirtualHost>
```

然后：

```bash
sudo mkdir -p /var/www/mysite
echo "MySite Home Page" | sudo tee /var/www/mysite/index.html
sudo systemctl restart httpd
```

---

## 8. 关闭 SELinux（测试时常用）

```bash
# 临时关闭
sudo setenforce 0

# 永久关闭（修改配置文件）
sudo sed -i 's/^SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```

---

## 9. 常见问题排查

| 问题                            | 可能原因                         | 解决方案                         |
|---------------------------------|----------------------------------|----------------------------------|
| 无法访问网站                   | 防火墙未开放80端口              | `firewall-cmd` 开启HTTP服务     |
| 页面显示 403 Forbidden         | 权限不足                         | 确保 `/var/www/html` 权限正确   |
| Apache 启动失败                | 配置文件语法错误                 | 使用 `apachectl configtest` 检查 |
| SELinux 拒绝访问               | SELinux 策略限制                 | 关闭 SELinux 或设置策略         |

---

## 小技巧：配置测试命令

```bash
# 检查配置语法
sudo apachectl configtest

# 查看监听端口
sudo netstat -tulnp | grep httpd
```

---

## 总结

CentOS 7 下部署 Apache Web 服务器涉及：

- 软件安装（`httpd`）
- 启动与开机自启设置
- 站点文件目录：`/var/www/html`
- 主配置文件：`/etc/httpd/conf/httpd.conf`
- 防火墙与 SELinux 的放行与关闭
- 虚拟主机配置支持多个站点部署

```bash
# 常用命令总结
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
```
