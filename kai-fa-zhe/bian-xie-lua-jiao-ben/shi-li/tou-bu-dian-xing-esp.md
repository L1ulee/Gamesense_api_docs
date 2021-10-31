# 头部点型ESP

如果启用此脚本，则会在敌人的头上绘制小点。如果头部不可见，则点为白色，如果可见则为红色

![](<../../../.gitbook/assets/image (4).png>)

```
-- 本地常用的API变量以提升性能,通常不这么做更好,但是Lua每次都必须将它们作为全局变量进行查找
local client_eye_position, client_trace_line, entity_get_local_player, entity_get_players, entity_hitbox_position, renderer_circle, renderer_world_to_screen = client.eye_position, client.trace_line, entity.get_local_player, entity.get_players, entity.hitbox_position, renderer.circle, renderer.world_to_screen

local function on_paint()
	local local_player = entity_get_local_player()
	local eye_x, eye_y, eye_z = client_eye_position()

	-- 获取所有存活玩家,非休眠(卡ESP)
	local enemies = entity_get_players(true)

	for i=1, #enemies do
		local entindex = enemies[i]

		-- 获取敌人头部hitbox的世界坐标
		local head_x, head_y, head_z = entity_hitbox_position(entindex, 0)

		-- 将世界坐标转换为屏幕坐标
		local wx, wy = renderer_world_to_screen(head_x, head_y, head_z)

		-- 确保始终检查屏幕坐标是否有效,只检查wx即可
			local r, g, b, a = 255, 255, 255, 100

			-- 从你的眼睛位置到敌人头部的光线追踪,忽略我们的本地玩家以确定它是否可见
			local fraction, entindex_hit = client_trace_line(local_player, eye_x, eye_y, eye_z, head_x, head_y, head_z)

			if entindex_hit == entindex or fraction == 1 then
				-- the trace either hit the enemy or hit nothing, meaning the head is visible, so we change the color
				r, g, b, a = 255, 16, 16, 255
			end

			-- draw circle with radius 4, so we offset the x and y by -2
			renderer_circle(wx-2, wy-2, r, g, b, a, 4, 0, 1)
		end
	end
end
client.set_event_callback("paint", on_paint)
```
