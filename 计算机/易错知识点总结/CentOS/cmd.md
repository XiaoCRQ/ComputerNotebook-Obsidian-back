# CentOS 7 常用命令汇总与示例

---

## 📁 文件与目录操作

- `ls`：列出文件
```bash
ls -l /etc
```

- `cd`：进入目录
```bash
cd /var/log
```

- `cp`：复制文件/目录
```bash
cp file1.txt /tmp/
```

- `mv`：移动/重命名文件
```bash
mv old.txt new.txt
```

- `rm`：删除文件/目录
```bash
rm -rf /tmp/test
```

- `mkdir`：创建目录
```bash
mkdir /opt/myapp
```

- `touch`：创建空文件
```bash
touch hello.txt
```

---

## 👤 用户与权限管理

- `useradd`：添加用户
```bash
useradd student
```

- `passwd`：设置密码
```bash
passwd student
```

- `usermod`：修改用户属性
```bash
usermod -aG wheel student  # 添加到sudo组
```

- `chown`：修改文件属主
```bash
chown root:root file.txt
```

- `chmod`：修改文件权限
```bash
chmod 755 script.sh
```

---

## 🔧 系统服务管理（systemd）

- 启动服务：
```bash
systemctl start httpd
```

- 停止服务：
```bash
systemctl stop firewalld
```

- 重启服务：
```bash
systemctl restart network
```

- 查看状态：
```bash
systemctl status sshd
```

- 设置开机启动：
```bash
systemctl enable mariadb
```

- 取消开机启动：
```bash
systemctl disable postfix
```

---

## 🌐 网络配置命令

- 查看 IP 地址：
```bash
ip addr
```

- 配置静态 IP（编辑配置文件）：
```bash
vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

- 重启网络服务：
```bash
systemctl restart network
```

- 测试连通性：
```bash
ping www.baidu.com
```

- DNS 配置文件：
```bash
/etc/resolv.conf
```

---

## 🔥 防火墙管理（firewalld）

- 查看状态：
```bash
firewall-cmd --state
```

- 开放端口：
```bash
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --reload
```

- 查看开放端口：
```bash
firewall-cmd --list-all
```

- 关闭防火墙（测试用）：
```bash
systemctl stop firewalld
```

---

## 📦 软件管理（YUM）

- 安装软件：
```bash
yum install httpd -y
```

- 删除软件：
```bash
yum remove vsftpd -y
```

- 搜索软件包：
```bash
yum search nginx
```

- 更新所有软件：
```bash
yum update -y
```

---

## 🔐 SELinux 管理

- 查看状态：
```bash
getenforce
```

- 设置为宽容模式（临时）：
```bash
setenforce 0
```

- 修改配置文件（永久）：
```bash
vi /etc/selinux/config
# SELINUX=disabled
```

---

## 📊 系统信息查看

- 查看当前用户：
```bash
whoami
```

- 查看内核版本：
```bash
uname -r
```

- 查看 CPU 信息：
```bash
lscpu
```

- 查看内存使用：
```bash
free -h
```

- 磁盘使用情况：
```bash
df -h
```

- 查看系统运行时间：
```bash
uptime
```

---

## 📋 日志查看命令

- 查看系统日志：
```bash
less /var/log/messages
```

- 查看开机日志：
```bash
journalctl -b
```

- 持续跟踪日志：
```bash
tail -f /var/log/messages
```

---

## 🧪 进程与性能监控

- 查看当前进程：
```bash
ps aux
```

- 动态查看系统资源：
```bash
top
```

- 查看指定服务端口监听情况：
```bash
netstat -tulnp | grep 80
```

---

## 📤 文件打包压缩

- 创建 tar 包：
```bash
tar -cvf backup.tar /etc
```

- 解压 tar 包：
```bash
tar -xvf backup.tar
```

- 打包并压缩：
```bash
tar -czvf backup.tar.gz /home/user
```

---

## 🧰 其他实用命令

- 查找文件：
```bash
find / -name httpd.conf
```

- 进程杀死：
```bash
kill -9 进程PID
```

- 定时任务（crontab）编辑：
```bash
crontab -e
```

- 查看当前计划任务：
```bash
crontab -l
```

---

以上命令涵盖了 **日常运维、用户管理、服务配置、网络调试、系统信息、日志查看等基本需求**，可用于考试、面试或日常使用的快速参考。
