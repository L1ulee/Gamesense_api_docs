---
description: 您可以使用client.set_event_callback监听的事件列表
---

# 事件

### 事件列表:

**paint(绘制)**

每次游戏在连接到服务器时渲染帧都会触发。可使用[renderer.\*](https://github.com/gamesensical/docs/blob/master/developers/globals/renderer/README.md)函数绘制到屏幕上

{% hint style="danger" %}
[链接失效，等待恢复...](https://github.com/gamesensical/docs/blob/master/developers/globals/renderer/README.md)
{% endhint %}

**示例:**

```
client.set_event_callback("paint", function()
	renderer.text(15, 15, 255, 255, 255, 255, nil, 0, "hello world")
end)
```

**paint\_ui(绘制UI)**

每次游戏渲染帧时触发，即使您在菜单中。可使用[renderer.\*](https://github.com/gamesensical/docs/blob/master/developers/globals/renderer/README.md)函数绘制到屏幕上

{% hint style="danger" %}
[链接失效，等待恢复...](https://github.com/gamesensical/docs/blob/master/developers/globals/renderer/README.md)
{% endhint %}

**run\_command(运行命令)**

当您还活着时，每次游戏运行命令(通常为每秒64次，等于tickrate)时触发。这是处理数据的最佳事件，这些数据仅在游戏从服务器收到更新时发生变化，例如有关玩家的信息

| key(关键词)            | 描述         |
| ------------------- | ---------- |
| **chokedcommands**  | 客户端阻塞的命令数量 |
| **command\_number** | 当前命令编号     |

**setup\_command(设置命令)**

每次游戏准备发送到服务器的移动命令时触发。这是在诸如AntiAim之类的作弊功能之前运行的，可用于修改用户输入(视角、按键、移动)如何被作弊看到。例如，设置`in_use = 1`将禁用AntiAim，就像在游戏中按下使用键一样。这是设定用户输入的首选方法与应该尽可能使用的`client.exec`

| key(关键词)                      | 描述                        |
| ----------------------------- | ------------------------- |
| **chokedcommands**            | 客户端阻塞的命令数量                |
| **command\_number**           | 当前命令编号                    |
| **pitch**                     | 俯仰视角                      |
| **yaw**                       | 偏航视角                      |
| **forwardmove**               | 前进/后退速度(-450 到 450)       |
| **sidemove**                  | 左/右速度(-450 到 450)         |
| **move\_yaw**                 | 用于运动的偏航角.如果未设置,则使用视图偏航    |
| **allow\_**_**send\_packet**_ | 设置为 false 使作弊杀死当前命令(如果可能) |
| **in\_attack**                | IN\_ATTACK 按钮             |
| **in\_jump**                  | IN\_JUMP 按钮               |
| **in\_duck**                  | IN\_DUCK 按钮               |
| **in\_forward**               | IN\_FORWARD 按钮            |
| **in\_back**                  | IN\_BACK 按钮               |
| **in\_use**                   | IN\_USE 按钮                |
| **in\_cancel**                | IN\_CANCEL 按钮             |
| **in\_left**                  | IN\_LEFT 按钮               |
| **in\_right**                 | IN\_RIGHT 按钮              |
| **in\_moveleft**              | IN\_MOVELEFT 按钮           |
| **in\_moveright**             | IN\_MOVERIGHT 按钮          |
| **in\_attack2**               | IN\_ATTACK2 按钮            |
| **in\_run**                   | IN\_RUN 按钮                |
| **in\_reload**                | IN\_RELOAD 按钮             |
| **in\_alt1**                  | IN\_ALT1 按钮               |
| **in\_alt2**                  | IN\_ALT2 按钮               |
| **in\_score**                 | IN\_SCORE 按钮              |
| **in\_speed**                 | IN\_SPEED 按钮              |
| **in\_walk**                  | IN\_WALK 按钮               |
| **in\_zoom**                  | IN\_ZOOM 按钮               |
| **in\_weapon1**               | IN\_WEAPON1 按钮            |
| **in\_weapon2**               | IN\_WEAPON2 按钮            |
| **in\_bullrush**              | IN\_BULLRUSH 按钮           |
| **in\_grenade1**              | IN\_GRENADE1 按钮           |
| **in\_grenade2**              | IN\_GRENADE2 按钮           |
| **in\_attack3**               | IN\_ATTACK3 按钮            |
| **weaponselect**              |                           |
| **weaponsubtype**             |                           |

**override\_view(覆盖视图)**

让您覆盖镜头位置和角度

| key(关键词)  | 描述     |
| --------- | ------ |
| **x**     | 镜头X 位置 |
| **y**     | 镜头Y位置  |
| **z**     | 镜头Z位置  |
| **pitch** | 俯仰视角   |
| **yaw**   | 偏航视角   |
| **fov**   | 视野     |

#### **console\_input(控制台输入)**

每次用户在游戏控制台中输入内容并按下回车键时触发。从事件处理程序返回true使游戏不处理输入

| 文本 | 属性      |
| -- | ------- |
| 1  | 控制台输入文本 |

**示例:**

```
client.set_event_callback("console_input", function(text)
	client.log("entered: '", text, "'")
end)
```

**output(输出)**

此事件可让您覆盖左上角绘制的文本。此事件只能有一个回调。此事件回调是从打印、client.log、client.color.log、"Missing due to spread"信息等调用的

{% hint style="warning" %}
确保在不需要时取消设置回调。否则，您将使用此事件破坏内置输出和其他脚本
{% endhint %}

| key(键)   | 描述             |
| -------- | -------------- |
| **text** | 绘制的文字          |
| **r**    | 绘制颜色:红色 0\~255 |
| **g**    | 绘制颜色:绿色 0\~255 |
| **b**    | 绘制颜色:蓝色 0\~255 |
| **a**    | 阿尔法 0\~255     |

**indicator(指示器光标)**

此事件让您可以覆盖指示器的绘制方式。此事件只能有一个回调。此事件回调是从renderer.indicator和indicator(如"DT")调用的

{% hint style="warning" %}
确保在不需要时取消设置回调。否则，您将使用此事件破坏内置指示器和其他脚本
{% endhint %}

| key(关键词) | 描述             |
| -------- | -------------- |
| **text** | 绘制的文字          |
| **r**    | 绘制颜色:红色 0\~255 |
| **g**    | 绘制颜色:绿色 0\~255 |
| **b**    | 绘制颜色:蓝色 0\~255 |
| **a**    | Alpha 0\~255   |

**player\_chat(玩家聊天)**

当玩家发送消息聊天时触发

| key(关键词)     | 描述                 |
| ------------ | ------------------ |
| **teamonly** | 如果消息被发送到团队聊天则为true |
| **entity**   | 发送消息的玩家的实体索引       |
| **name**     | 发送消息的玩家名称          |
| **text**     | 聊天消息文本             |

**string\_cmd(字符串命令)**

在将字符串命令(聊天信息、武器检查、购买命令)发送到服务器前触发

| Text(文本) | Property |
| -------- | -------- |
| 1        | 字符串命令    |

**net\_**_**update**_**\_start**

在游戏处理来自服务器的实体更新的数据包之前触发

(`FrameStageNotify FRAME_`_`NET_UPDATE`_`_START`)

{% hint style="warning" %}
`使用此事件修改实体数据时要小心，有些东西必须手动恢复，即使完全更新后也不会更新它们!`
{% endhint %}

**net\_update\_end**

从服务器接收实体更新的数据包之后触发

(`FrameStageNotify FRAME_`_`NET_`_`UPDATE_END`)

**predict\_command(预判命令)**

在游戏中预判时触发

{% hint style="info" %}
这个事件在每秒被调用很多次，避免在其中进行任何复杂的处理
{% endhint %}

|  key(关键词)       | 描述        |
| --------------- | --------- |
| command\_number | 预判命令的命令号码 |
