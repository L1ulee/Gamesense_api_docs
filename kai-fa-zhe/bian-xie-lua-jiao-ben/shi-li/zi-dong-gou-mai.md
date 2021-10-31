# 自动购买

此脚本在"MISC"中添加了一个"Auto buy AWP"的复选框，当AWP被限制购买数量时使用很方便(游玩HVH时)

```
local ui_get, console_cmd = ui.get, client.exec

local auto_buy_awp = ui.new_checkbox("MISC", "Miscellaneous", "Auto buy AWP")

local function on_round_prestart(e)
	if ui_get(auto_buy_awp) then
		console_cmd("buy awp;")
	end
end
client.set_event_callback("round_prestart", on_round_prestart)
```
