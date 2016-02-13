RClient: LuaJIT Client for Rserve
=================================

LuaJIT client for [Rserve](http://www.rforge.net/Rserve/) which is used to host a (local or remote) R session toward which a connection is established.

## Features

- exchange data between LuaJIT and R (arrays, matrices, lists, data.frames)
- execute arbitrary R code from LuaJIT

```lua
local R = require "rclient"
  
local r = R.connect()
  
-- Lua --> R:
r.myvec  = { 1,2,3 } -- Array.
r.mymat  = R.asmatrix({ {1,2,3},{4,5,6} })
r.mylist = R.aslist({ 7,8,9 }, { "a","b","c" })
r.mydf   = R.asdataframe({ 7,8,9 }, { "a","b","c" }, { "row1" })
  
-- Execute R commands and evaluate expression as in R interpreter:
r "myvec <- myvec^2"
r "myvec" --> [1] 1 4 9
 
-- R --> Lua:
local vec  = r.myvec
local mat  = r.mymat
local list = r.mylist
local df   = r.mydf
print(unpack(vec))    --> 1 4 9
print(unpack(mat[1])) --> 1 2 3
print(unpack(mat[2])) --> 4 5 6
print(unpack(list[0][1]))                 --> a b c
print(list[1][1], list[2][1], list[3][1]) --> 7 8 9
print(list.a[1],  list.b[1],  list.c[1] ) --> 7 8 9
print(unpack(df[0][1]))             --> a b c
print(unpack(df[0][2]))             --> row1
print(df[1][1], df[2][1], df[3][1]) --> 7 8 9
print(df.a[1],  df.b[1],  df.c[1] ) --> 7 8 9
```

## Install

This module is included in the [ULua](http://ulua.io) distribution, to install it use:
```
upkg add rclient
```

Alternatively, manually install this module making sure that all dependencies listed in the `require` section of [`__meta.lua`](__meta.lua) are installed as well (dependencies starting with `clib_` are standard C dynamic libraries).

## Documentation

Refer to the [official documentation](http://scilua.org/rclient.html).
