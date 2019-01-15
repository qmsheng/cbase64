# cbase64

基于c封装so库，供ngx_lua调用


可以根据需求跟换编码/解码表



# 应用示例：
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
	str = str or 'Jw94OIrQFIJmF84wX5E8XIE9X8u5JVE8Nw94OIuUB_r3g8r5FzKDdzkLE5gGYzcadNY9Nw94OlY8J1aLX8x3E593OIFQt8rGBljQXI4WXI-mEAKUOIrag8kVg8-wBIJ5FwCLX89vY_E9g5K4B_c4Y_FwgUxRFwK4gwrmB1kUX_T5gI98BIxUBzuUBk='

	local gen_key = ffi_new("unsigned char[?]", #str)
	ffi_copy(gen_key, str, #str)

    local result = libcbase64.base64_decode(gen_key)
    return ffi_str(result)
end

return _M

