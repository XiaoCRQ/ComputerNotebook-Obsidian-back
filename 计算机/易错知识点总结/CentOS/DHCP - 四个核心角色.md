# 📌 DHCP 四个核心角色详解（Client、Server、Relay、Discover）

---

## 🖥️ 1. DHCP Client（客户端）

### 💡 定义  
发起 DHCP 请求的设备，通常是终端用户的计算机、手机或打印机。

### 🧭 作用  
向网络广播请求 IP 地址和其他网络配置信息。

### 📤 行为  
- 启动网络后，自动发送 DHCP Discover 报文  
- 接收 Server 的 Offer，并发起 Request 请求

### 🧪 示例  
```text
电脑开机后，自动获取 192.168.1.105 地址
```

---

## 🗄️ 2. DHCP Server（服务器）

### 💡 定义  
提供 IP 地址及网络参数的设备或服务，常运行在网络中的专用服务器上。

### 🧭 作用  
响应客户端请求，分配地址并返回相关配置。

### 📥📤 行为  
- 接收 Discover 报文  
- 回复 Offer → 等待 Request → 发送 ACK 确认

### 🧪 示例  
```text
分配 IP 范围：192.168.1.100 - 192.168.1.200
网关：192.168.1.1，DNS：8.8.8.8
```

---

## 🔁 3. DHCP Relay（中继代理）

### 💡 定义  
转发 DHCP 请求与响应报文的网络设备（如路由器），用于跨子网访问 DHCP Server。

### 🧭 作用  
中转 Discover 和 Request 报文至远程 Server，再将响应返回 Client。

### 📤 行为  
- 接收到本地广播的 Discover 报文  
- 修改为单播转发给 Server（使用 `giaddr` 标识来源网络）

### 🧪 示例  
```text
Client IP: 192.168.2.10 → DHCP Server 在 192.168.1.1（不同子网）
Router 作为中继转发 Discover 报文
```

---

## 📣 4. DHCP Discover（发现报文）

### 💡 定义  
客户端发出的首个 DHCP 广播报文，请求网络配置。

### 🧭 作用  
让 DHCP Server 知道客户端需要获取 IP 地址。

### 🧾 报文内容  
- 源 IP（0.0.0.0），广播目标（255.255.255.255）  
- 包含 MAC 地址作为标识  
- 不指定目标 Server

### 🧪 示例  
```text
Client → Broadcast → “谁能给我 IP 地址？”
```

---

## 🧠 总结表

| 角色       | 功能描述                           | 通信方向               |
|------------|------------------------------------|------------------------|
| Client     | 请求 IP 的终端设备                 | 发起 Discover 请求    |
| Server     | 分配 IP 和网络参数的服务端         | 回复 Offer → ACK      |
| Relay      | 中继转发 DHCP 报文的设备           | 转发 Discover / Offer |
| Discover   | 客户端广播的“请求地址”报文        | Client → 广播网络     |

> 📌 **掌握这四个角色是理解 DHCP 机制的基础**，特别是在跨网段部署或排错时，理解 Relay 的作用至关重要。
