# 🛰️ Wifite 使用教程（适用于 Arch Linux）

`wifite` 是一个自动化无线网络攻击脚本，它集成了多个工具（如 `aircrack-ng`、`reaver`、`bully` 等），支持对 WPA/WPA2 网络进行握手捕获与密码破解，也可攻击开启 WPS 的网络。

---

## ✅ 前提条件

- Arch Linux 或其他支持 `pacman`/`yay` 的系统
- 支持监控模式的无线网卡
- 运行脚本时具有 `root` 权限

---

## 🧰 安装 Wifite 及相关依赖

推荐使用 `pacman` 安装：

```bash
sudo pacman -S wifite aircrack-ng reaver
```

可选工具（用于增强功能）：

```bash
yay -S bully pyrit hashcat cowpatty
```

---

## 📡 启动无线网卡监控模式

使用 `airmon-ng` 启用监控模式：

```bash
sudo airmon-ng start wlan0
```

> ⚠️ `wlan0` 可能是 `wlp3s0`、`wlan1` 等，请用 `ip a` 确认接口名称。

---

## 🚀 启动 Wifite

直接运行命令：

```bash
sudo wifite
```

程序将自动开始扫描周围的 WiFi 网络。你可以使用方向键选中目标网络并按回车进行攻击。

---

## 🔍 攻击方式说明

Wifite 默认尝试以下方式（可配置）：

- 捕获 WPA/WPA2 握手包，并使用字典破解
- 如果目标开启了 WPS，尝试使用 `reaver` 或 `bully` 暴力破解 PIN
- 自动跳过信号弱或不可用的目标

---

## ⚙️ 常用选项

| 参数 | 说明 |
|------|------|
| `--kill` | 自动杀死干扰网络的进程（推荐） |
| `--no-wpa` | 不攻击 WPA/WPA2 网络 |
| `--wps-only` | 仅攻击开启 WPS 的网络 |
| `--dict <路径>` | 指定密码字典路径 |
| `--timeout <秒>` | 设置每个目标攻击超时时间 |
| `--power <dBm>` | 过滤信号强度低的目标 |

示例：指定字典文件攻击 WPA 网络：

```bash
sudo wifite --dict /usr/share/wordlists/rockyou.txt
```

---

## 🔓 破解 WPA 密码（通过字典）

Wifite 会将握手包保存至 `hs/` 目录。可使用 `aircrack-ng` 手动破解：

```bash
aircrack-ng hs/*.cap -w /usr/share/wordlists/rockyou.txt
```

---

## 🛑 停止监控模式

完成攻击后关闭监控模式：

```bash
sudo airmon-ng stop wlan0mon
```

---

## 📁 默认文件保存位置

- 握手文件：`hs/*.cap`
- 日志文件：`hs/*.log`
- 破解结果：终端输出或日志中

---

## 🧠 注意事项

- 合法使用：**请仅用于测试您拥有权限的网络**
- 网络接口需支持注入（monitor + injection）
- 有些目标路由器启用防护机制（如防WPS攻击）

---

## 📚 参考资源

- [Wifite GitHub](https://github.com/derv82/wifite)
- [aircrack-ng 官方文档](https://www.aircrack-ng.org/documentation.html)

---

> ⚠️ 本教程仅用于学习与授权测试目的，禁止用于非法用途！
