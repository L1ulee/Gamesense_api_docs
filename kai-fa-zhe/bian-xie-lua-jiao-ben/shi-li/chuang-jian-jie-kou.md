# 创建接口

此脚本是"client.create\_interface"的示例。使用此功能，您可以访问游戏本身提供的类或功能

```
local ffi = require 'ffi'

ffi.cdef[[
    typedef unsigned char wchar_t;

    typedef bool (__thiscall *IsButtonDown_t)(void*, int);
]]
local interface_ptr = ffi.typeof('void***')

local raw_inputsystem = client.create_interface('inputsystem.dll', 'InputSystemVersion001')

-- 将 lightuserdata 转换为我们可以取消引用的类型
local inputsystem = ffi.cast(interface_ptr, raw_inputsystem) -- void***

-- 取消引用接口指针以获取 vtable
local inputsystem_vtbl = inputsystem[0] -- void**

-- vtable 是一个函数数组,第15个是 IsButtonDown
local raw_IsButtonDown = inputsystem_vtbl[15] -- void*

-- 将函数指针转换为可调用类型
local is_button_pressed = ffi.cast('IsButtonDown_t', raw_IsButtonDown)

local function run_command(cmd)
    if is_button_pressed(inputsystem, 36) then -- ButtonCode_t for Z
        print('Z is pressed')
    end
    return false
end

client.set_event_callback('run_command', run_command)
```
