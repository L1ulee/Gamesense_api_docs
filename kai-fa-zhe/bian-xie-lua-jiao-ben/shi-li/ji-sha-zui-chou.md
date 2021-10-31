# 击杀嘴臭

每次当您击杀某个人时，此脚本都会在聊天中自动键入一条消息。如果是爆头，则显示"one tap"，否则显示"ez"

```
local userid_to_entindex, get_local_player, is_enemy, console_cmd = client.userid_to_entindex, entity.get_local_player, entity.is_enemy, client.exec

local function on_player_death(e)
	local victim_userid, attacker_userid = e.userid, e.attacker
	if victim_userid == nil or attacker_userid == nil then
		return
	end

	local victim_entindex = userid_to_entindex(victim_userid)
	local attacker_entindex = userid_to_entindex(attacker_userid)

	if attacker_entindex == get_local_player() and is_enemy(victim_entindex) then
		console_cmd("say ", e.headshot and "one tap" or "ez")
	end
end
client.set_event_callback("player_death", on_player_death)
```
