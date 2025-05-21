# ASUS UEFI BIOS 总结笔记

## 1. 进入 BIOS

- 按 `Delete` 或 `F2`（POST 期间）进入 BIOS 设置界面
- 也可在开机自检后按 `Esc` 调出启动菜单，再选择进入 BIOS

## 2. 模式切换

### 简易模式 (EZ Mode)

- 默认界面，展示系统概览（CPU 温度、电压、风扇转速、内存频率等）
- 按 `F7` 或点击 “Advanced Mode” 切换至高级模式

### 高级模式 (Advanced Mode)

- 完整分区：Main、Ai Tweaker、Advanced、Monitor、Boot、Tool、Exit
- 按 `F7` 或点击 “EZ Mode” 返回简易模式

## 3. 导航与热键

- 方向键 (↑↓←→)：移动光标
- `Enter`：确认或进入子菜单
- - / –：调整选项数值或枚举
- `F1`：显示当前项帮助
- `F5`：加载优化默认设置
- `F7`：切换简易/高级模式
- `F10`：保存并退出
- `Esc`：返回上级或退出 BIOS

## 4. 菜单模块总览

- **Main**
  - System Date（系统日期）
  - System Time（系统时间）
  - Language（语言设置）
- **Ai Tweaker**
  - AI Overclock Tuner（AI 超频调谐）
  - D.O.C.P.（内存配置）
  - BCLK Frequency（基础时钟频率）
- **Advanced**
  - CPU Configuration（CPU 配置）
  - SATA Configuration（SATA 配置）
  - USB Configuration（USB 配置）
- **Monitor**
  - CPU Temperature（CPU 温度）
  - Voltages（电压监控）
  - Fan Speed（风扇转速）
- **Boot**
  - Boot Option Priorities（启动项优先级）
  - CSM (Compatibility Support Module)（兼容性支持模块）
- **Tool**
  - ASUS EZ Flash 3（在线/离线刷写 BIOS）
  - OC Profile（超频配置文件管理）
- **Exit**
  - Save Changes & Reset（保存更改并重启）
  - Discard Changes & Exit（放弃更改并退出）
  - Load Optimized Defaults（加载优化默认设置）
- **My Favorites（收藏夹）**
  - 按 `F3` 或点击顶部 “My Favorites”
  - 右键任意选项 → “Add to Favorites” 添加到收藏
  - 页面底部可 “Recover to default favorite items” 恢复默认
- **Summary / Overview（概要）**
  - 仅在简易模式下可见
  - 实时显示 CPU/主板温度、电压、风扇转速、SATA 设备等
  - 点击 “`” “`” 切换 EZ System Tuning 预设模式
  - 可快速加载优化默认或进入 Q-Fan 风扇控制

## 5. 收藏与退出

- 按 `F3` 打开/关闭“收藏夹”面板
- 按 `F10` 保存所有更改并退出 BIOS
- 按 `Esc` 放弃更改或返回上级
