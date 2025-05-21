# CentOS 7 用户控制相关操作与知识点

---

## 👤 一、用户管理命令
[CentOS目录](CentOS目录.md)
- 添加用户：
```bash
useradd 用户名
```

- 设置密码：
```bash
passwd 用户名
```

- 修改用户信息：
```bash
usermod -c "备注" -s /bin/bash -d /home/newhome 用户名
```

- 删除用户：
```bash
userdel 用户名
userdel -r 用户名  # 连同主目录一起删除
```

- 查看用户信息：
```bash
id 用户名
finger 用户名
```

---

## 👥 二、用户组管理

- 添加组：
```bash
groupadd 组名
```

- 删除组：
```bash
groupdel 组名
```

- 将用户添加到组：
```bash
usermod -aG 组名 用户名
```

- 修改主组：
```bash
usermod -g 新主组 用户名
```

- 查看用户所在组：
```bash
groups 用户名
```

- 查看所有组：
```bash
cut -d: -f1 /etc/group
```

---

## 📁 三、文件权限与属主管理

### 权限字符说明：

| 字符 | 含义        |
|------|-------------|
| r    | 读权限      |
| w    | 写权限      |
| x    | 执行权限    |
| -    | 无权限      |
| d    | 目录        |
| l    | 软链接      |

### 修改文件属主属组：

```bash
chown 用户名:组名 文件
```

### 修改文件权限：

```bash
chmod 755 文件
```

> 示例：`chmod u=rwx,g=rx,o=r filename`

---

## 🔑 四、用户密码与安全管理

- 强制用户下次登录修改密码：
```bash
chage -d 0 用户名
```

- 设置密码有效期：
```bash
chage -M 90 用户名   # 最大有效期90天
chage -m 7 用户名    # 最小间隔7天
chage -W 7 用户名    # 提前7天警告
```

- 查看密码策略：
```bash
chage -l 用户名
```

- 锁定用户账号：
```bash
usermod -L 用户名
```

- 解锁用户账号：
```bash
usermod -U 用户名
```

---

## 🧱 五、用户配额（磁盘限制）

### 1. 安装工具

```bash
yum install quota -y
```

### 2. 修改 `/etc/fstab` 启用配额

```conf
UUID=xxx  /home  ext4  defaults,usrquota,grpquota  0 0
```

重启或重新挂载：

```bash
mount -o remount /home
```

### 3. 建立配额数据库

```bash
quotacheck -cum /home
```

### 4. 启用配额功能

```bash
quotaon /home
```

### 5. 设置用户配额

```bash
edquota 用户名
```

> 编辑内容示例：

```
Soft limit: 100000
Hard limit: 120000
```

---

## 🔒 六、系统用户与普通用户区别

| 类型       | UID 范围      | 说明                          |
|------------|----------------|-------------------------------|
| 系统用户   | 0–999          | 用于服务、系统进程           |
| 普通用户   | 1000 以上      | 实际登录系统的人类用户       |
| root       | UID=0          | 拥有最高权限的超级用户       |

---

## 📄 七、重要文件路径说明

| 文件路径               | 用途说明                      |
|------------------------|-------------------------------|
| `/etc/passwd`          | 存储所有用户的基本信息        |
| `/etc/shadow`          | 存储用户加密后的密码          |
| `/etc/group`           | 存储用户组信息                |
| `/etc/gshadow`         | 存储组密码等敏感信息          |
| `/home/用户名/`        | 普通用户主目录                |
| `/etc/login.defs`      | 默认用户账号策略              |
| `/etc/skel/`           | 用户默认主目录模板文件        |

---

## ✅ 八、示例操作流程

### 添加用户 user1，加入 wheel 组，设置密码并强制改密：

```bash
useradd -G wheel user1
passwd user1
chage -d 0 user1
```

### 锁定用户 user2：

```bash
usermod -L user2
```

### 删除用户 user3 及其主目录：

```bash
userdel -r user3
```

---

以上内容覆盖了 CentOS 7 系统中关于用户管理的日常操作及重要知识点。适合用于系统管理、RHCSA 学习、实验操作和笔记归纳。
