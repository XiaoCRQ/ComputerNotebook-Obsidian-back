# 新建作用域

- `管理工具` —— `DHCP`
- 进入服务器右击 `IPv4 / IPv6`
- `新建作用域` 选项
![](../../../Resource/Pasted%20image%2020250521154220.png)
- 设置 
![](../../../Resource/Pasted%20image%2020250521154408.png)
![](../../../Resource/Pasted%20image%2020250521154443.png)

![](../../../Resource/Pasted%20image%2020250521154628.png)![](../../../Resource/Pasted%20image%2020250521154648.png)![](../../../Resource/Pasted%20image%2020250521154723.png)![](../../../Resource/Pasted%20image%2020250521154737.png)![](../../../Resource/Pasted%20image%2020250521154750.png)

# 常规选项

![](../../../Resource/Pasted%20image%2020250521154821.png)
- 地址池 
>分配地址范围
- 地址租用
>已租用地址
- 保留
>设置静态地址
- 作用域选项
> 设置DNS等服务器策略
- 策略 —— 同上
- 服务器选项 —— 同上
- 筛选器
> 允许/禁止
![](../../../Resource/Pasted%20image%2020250521155257.png)

> [!WARNING]
> 如果只有 `特定` 机器才可以分配 `IP` ，则需要收集 `MAC` 地址， 新建 `筛选器`
> 若需动态配置 `默认网关` 和 `DNS` 服务器，则需在 `作用域选项` 中配置
> `DHCP` 在分配 `IP` 时，第一次分配使用 `广播` ， 后续续期 `单播`

