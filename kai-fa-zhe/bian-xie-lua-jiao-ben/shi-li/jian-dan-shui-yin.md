# 简单水印

这是一个简单的文本水印，显示了Ping，Tickrice和Windwos时间。在游戏中它看起来这样:

![](<../../../.gitbook/assets/image (9).png>)

修改`flags`，`margin`和`padding`变量以修改外观。颜色在2个绘图函数调用中被硬编码，但也可以轻松修改

```
-- 本地常用的API变量以提升性能,通常不这么做更好,但是Lua每次都必须将它们作为全局变量进行查找
local client_latency, client_screen_size, client_system_time, globals_tickinterval, math_floor, renderer_measure_text, renderer_rectangle, renderer_text, string_format = client.latency, client.screen_size, client.system_time, globals.tickinterval, math.floor, renderer.measure_text, renderer.rectangle, renderer.text, string.format

-- 每次CS:GO渲染一帧并在您的游戏中绘制时,都会执行此函数
local function on_paint()
	-- 获取动态信息获取.延迟以秒为单位,因此我们将其转换为毫秒并将其舍入.Tick率用1 / Tick间隔计算
	local screen_width, screen_height = client_screen_size()
	local latency = math_floor(client_latency()*1000+0.5)
	local tickrate = 1/globals_tickinterval()
	local hours, minutes, seconds = client_system_time()

	-- 创建文本
	local text = string_format("%dms", latency) .. " | " .. string_format("%dtick", tickrate) .. " | " .. string_format("%02d:%02d:%02d", hours, minutes, seconds)

	-- 修改这些以更改文本的显示方式.margin是与右上角的距离,padding是背景矩形大于文本的大小
	local margin, padding, flags = 18, 4, nil

	-- 取消"small and capital"风格的注释
	-- flags, text = "-", (text:upper():gsub(" ", "   "))

	-- measure text size to properly offset the text from the top right corner
	local text_width, text_height = renderer_measure_text(flags, text)

	-- draw background and text
	renderer_rectangle(screen_width-text_width-margin-padding, margin-padding, text_width+padding*2, text_height+padding*2, 32, 32, 32, 200)
	renderer_text(screen_width-text_width-margin, margin, 235, 235, 235, 255, flags, 0, text)
end
client.set_event_callback("paint", on_paint)
```
