# cbase64

基于c封装so库，供ngx_lua调用


可以根据需求更换编码/解码表



# 应用示例：
```lua
local _M = {
    _VERSION = '0.01'
}

local ffi = require "ffi"
local ffi_new = ffi.new
local ffi_str = ffi.string
local ffi_copy = ffi.copy

ffi.cdef[[
    unsigned char *base64_decode(unsigned char *code);
]]

local libcbase64 = ffi.load("libcbase64")


function _M.base64_decode(str)
	str = str or ''

	local gen_key = ffi_new("unsigned char[?]", #str)
	ffi_copy(gen_key, str, #str)

    local result = libcbase64.base64_decode(gen_key)
    return ffi_str(result)
end

return _M
```

