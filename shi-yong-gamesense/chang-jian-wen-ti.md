# 常见问题

### 内存不足(Out of memory)

1.您的计算机已经运行了很长时间并且物理内存已经碎片化

2.进程或驱动程序正在使用大部分物理内存

尝试关闭使用大量内存的程序，或者重新启动计算机

### 杀毒软件(AntiVirus)

一些杀毒软件提供非常严格的实时监控/沙盒，这可能会影响客户端。您无需禁用Windows Defender。确保关闭杀毒软件并卸载其驱动程序。您可以在注入后重新打开它们

{% hint style="info" %}
**已知的不兼容厂家: **Trend Micro, F-Secure, MalwareBytes
{% endhint %}

### Windows版本不受支持(Unsupported version of Windows)

需要Windows 8.1及更高版本，某些较旧的Windows 10可能无法运行，请更新到最新版本的Windwos10。如果您使用的是Windows 10.0.14393或更高版本并且收到此错误，请重新启动计算机并重试

### 反作弊(Anti-Cheat)

一些反作弊驱动程序(特指BattleEye)保护的游戏/Steam进程可能导致出现问题

### 叠加面板(Overlay)/第三方工具(Third party tool)

任何影响游戏渲染的软件都可能导致问题

{% hint style="info" %}
**已知的不兼容软件: **Fraps, SweetFX, Discord Overlay, NZXT CAM

**产生的错误代码: **无，游戏会直接崩溃
{% endhint %}

### "不支持虚拟机"("Virtual machine not supported")

一些杀毒软件会在虚拟机(沙盒)中运行程序，如果您没有使用杀毒软件，请确保禁用Hyper-V

![](<../.gitbook/assets/image (4) (1).png>)

{% hint style="info" %}
**已知的不兼容软件: **HitmanPro.Alert
{% endhint %}

### 客户端打不开?

如果打开客户端时没有任何反应，请尝试启用UAC(用户账户控制)并重新启动Steam。将其设置为默认设置，即下图

![](<../.gitbook/assets/image (7).png>)

### 菜单显示为纯黑色矩形

在CS:GO设置中启用"多核渲染"

### 菜单不显示或闪烁

从启动选项中删除"nod3d9ex"

确保Steam覆盖启用。在以下两个位置检查是否启用:

Steam->设置->游戏中。在游戏中勾选"在游戏中启用Steam界面"

![](../.gitbook/assets/image.png)

右键库中的CS:GO->选择属性->通用。勾选"在游戏中启用Steam界面"

![](<../.gitbook/assets/image (3).png>)

### "过OBS检测(Hide from OBS)"不起作用

关闭或禁用Razer Synapse

在NVDIA控制面板中，转到"管理3D设置"并确保以下选项与您的全局设置相匹配:

平滑处理-FXAA-\[关]

平滑处理-模式-\[应用程序控制]

多帧采样AA(MFAA)-\[关]

着色器缓存-\[开]

纹理过滤-各向异性采样优化-\[关]

纹理过滤-负LOD偏移-\[允许]

纹理过滤-质量-\[质量]

纹理过滤-三线性优化-\[开]

线程优化-\[自动]

三重缓冲-\[关]

垂直同步-\[使用3D应用程序设置]

{% hint style="warning" %}
**确保"程序设置"中的CS:GO设置没有冲突**
{% endhint %}

### **初始化失败 \***

如果您玩过BattleEye或EAC保护的游戏就会发生这种情况，可通过重新启动计算机或禁用BE/EAC服务解决

### 客户端打开后立即关闭

安装您订阅(Subscription)的游戏，确保Windows版本为Windows 8.1或更高版本

## 常见错误代码

| 代码       | 描述                                                                                                   |
| -------- | ---------------------------------------------------------------------------------------------------- |
| D0001409 | [内存不足](chang-jian-wen-ti.md#nei-cun-bu-zu-out-of-memory)                                             |
| C000009A |                                                                                                      |
| D0001600 | [杀毒软件](chang-jian-wen-ti.md#sha-du-ruan-jian-antivirus)                                              |
| D0002001 |                                                                                                      |
| C0000022 |                                                                                                      |
| C00000F1 |                                                                                                      |
| C0000043 |                                                                                                      |
| C0000077 | [Windows版本不受支持](chang-jian-wen-ti.md#windows-ban-ben-bu-shou-zhi-chi-unsupported-version-of-windows) |
| D0002103 |                                                                                                      |
| D0001418 | [反作弊](chang-jian-wen-ti.md#fan-zuo-bi-anticheat)                                                     |
| D000210A |                                                                                                      |
| D0002201 | 连接问题                                                                                                 |
| D0001434 | 游戏加载时间过长，使用-novid或等到大厅注入                                                                             |
| C0000225 |                                                                                                      |
| D0001442 | 加载游戏时崩溃                                                                                              |
| D0001012 | ["不支持虚拟机"](chang-jian-wen-ti.md#bu-zhi-chi-xu-ni-ji-virtual-machine-not-supported)                   |
