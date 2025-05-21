i# 安装

- 开始菜单
- 服务器管理器
- 管理
- 添加角色和功能
![](../../../Resource/Pasted%20image%2020250426194538.png)
- 选择到服务器角色
- Web服务器(IIS)
![](../../../Resource/Pasted%20image%2020250426194620.png)
- 选择安装
![](../../../Resource/Pasted%20image%2020250426194821.png)

# 启动 

- 开始菜单
- 管理工具
- Internet Information Services(IIS)管理器
![](../../../Resource/Pasted%20image%2020250426194905.png)

# FTP 服务器

- 右击网站
- 添加FTP站点
![](../../../Resource/Pasted%20image%2020250426195029.png)
- 配置 【注意默认物理路径】
![](../../../Resource/Pasted%20image%2020250426195122.png)
- 配置SSL配置
![](../../../Resource/Pasted%20image%2020250426195215.png)
- 身份验证和授权信息
![](../../../Resource/Pasted%20image%2020250426195323.png)![](../../../Resource/Pasted%20image%2020250426195408.png)

## 基础界面
![](../../../Resource/Pasted%20image%2020250426195442.png)

## FTP IP 地址和域限制
![](../../../Resource/Pasted%20image%2020250426195638.png)

##FTP SSL 设置
![](../../../Resource/Pasted%20image%2020250426195658.png)

## FTP 防火墙支持
![](../../../Resource/Pasted%20image%2020250426195749.png)

## FTP目录浏览
![](../../../Resource/Pasted%20image%2020250426195820.png)
## FTP 请求筛选
![](../../../Resource/Pasted%20image%2020250426195858.png)

## FTP 授权规则
![](../../../Resource/Pasted%20image%2020250426195956.png)

# Web 服务器

- 右击网站
- 添加网站
![](../../../Resource/Pasted%20image%2020250426200132.png)
- 配置网站 【注意默认地址】
![](../../../Resource/Pasted%20image%2020250426200222.png)

## 基础界面
![](../../../Resource/Pasted%20image%2020250426201201.png)

## 默认文档
![](../../../Resource/Pasted%20image%2020250426201254.png)

> 其他如上

# 相关常识

## FTP

- FTP的默认路径
	c:\inetpub\ftproot

- 端口
	数据：20
	控制：21

## WWW

- 默认站点名称
	Default web site

- Web的默认路径
	c:\inetpub\wwwroot

- 端口
	HTTP：80
	HTTPS：443

## 错误页
| 状态码 | 含义                    | 简单解释             |
| --- | --------------------- | ---------------- |
| 200 | OK                    | 一切正常，网页成功返回。     |
| 301 | Moved Permanently     | 永久重定向，网页地址变了。    |
| 302 | Found                 | 临时重定向，暂时换了个地址。   |
| 400 | Bad Request           | 请求错误，服务器听不懂你的请求。 |
| 401 | Unauthorized          | 没有权限，通常需要登录。     |
| 403 | Forbidden             | 禁止访问，你没权限看这个内容。  |
| 404 | Not Found             | 页面不存在，地址打错了？     |
| 500 | Internal Server Error | 服务器内部出错，程序炸了。    |
| 502 | Bad Gateway           | 服务器作为网关收到错误响应。   |
| 503 | Service Unavailable   | 服务暂时不可用，服务器累了。   |
**小技巧记忆：**

- 2xx 是成功
    
- 3xx 是重定向
    
- 4xx 是客户端错误（你的请求有问题）
    
- 5xx 是服务器错误（服务器自己出问题了）
