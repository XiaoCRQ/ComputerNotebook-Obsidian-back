# CentOS 7 配置 FTP 服务器（vsftpd）

---

## 1. 安装 vsftpd

```bash
sudo yum install -y vsftpd
```

---

## 2. 配置主文件

主配置文件路径：

```
/etc/vsftpd/vsftpd.conf
```

### 推荐修改内容：

```conf
# 允许本地用户登录
local_enable=YES

# 允许上传文件
write_enable=YES

# 启用 chroot 限制用户访问自己的目录
chroot_local_user=YES

# 允许匿名访问（可选）
anonymous_enable=NO

# 支持被动模式端口（防火墙环境推荐开启）
pasv_enable=YES
pasv_min_port=30000
pasv_max_port=31000
```

✅ 修改完毕后保存退出。

---

## 3. 启动并设置开机自启

```bash
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```

---

## 4. 防火墙设置

```bash
sudo firewall-cmd --permanent --add-service=ftp
sudo firewall-cmd --permanent --add-port=30000-31000/tcp
sudo firewall-cmd --reload
```

---

## 5. SELinux 设置（可选）

开启上传功能时，需执行：

```bash
sudo setsebool -P ftpd_full_access 1
```

---

## 6. 创建 FTP 用户及目录

```bash
sudo useradd ftpuser
sudo passwd ftpuser
```

创建访问目录并设置权限：

```bash
sudo mkdir -p /home/ftpuser/ftp_files
sudo chown -R ftpuser:ftpuser /home/ftpuser/ftp_files
```

默认登录目录是用户的 `/home/用户名/`，可根据需要修改配置项 `local_root=/指定路径`。

---

## 7. 测试登录

在客户端或浏览器中输入：

```bash
ftp://服务器IP
```

使用用户名和密码登录。也可以使用 `ftp` 命令行客户端或图形工具（如 FileZilla）。

---

## 8. 常见问题与排查

| 问题                             | 可能原因                      | 解决方法                          |
|----------------------------------|-------------------------------|-----------------------------------|
| 登录后无法上传文件               | `write_enable=YES` 未设置     | 修改配置并重启服务                |
| 用户无法切换目录或被拒绝登录     | `chroot_local_user=YES` 缺失  | 添加并重启                        |
| 登录失败提示 530                 | 用户目录无权限或 SELinux 限制 | 检查权限并使用 `setsebool`        |
| 浏览器打不开                     | 防火墙未开放端口或被动端口    | 配置防火墙                        |

---

## 9. 附加配置项说明

| 配置项                | 含义                                               |
|-----------------------|----------------------------------------------------|
| anonymous_enable      | 是否启用匿名登录                                   |
| local_enable          | 是否允许本地用户登录                               |
| write_enable          | 是否允许上传文件                                   |
| chroot_local_user     | 是否限制用户访问其主目录                           |
| pasv_enable           | 是否启用被动模式（配合防火墙环境使用）            |
| pasv_min_port / max   | 被动模式数据传输端口范围                           |
| local_root            | 指定用户登录的默认目录                             |
| listen                | 是否以独立服务模式监听（默认为 YES）              |

---

## 10. 查看日志（调试用）

```bash
tail -f /var/log/vsftpd.log
```

---

## 快速排错汇总

```bash
# 重启服务
sudo systemctl restart vsftpd

# 查看运行状态
sudo systemctl status vsftpd

# 查看监听端口
sudo netstat -tulnp | grep :21

# SELinux 相关设置
sudo setsebool -P ftpd_full_access 1
```
