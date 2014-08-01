Rclient
=======

This is a client for the Rserve package of the R statistical programming language released under the MIT license. Rserve is used to host an R session toward which connections can be established both locally and remotely. The Rclient library makes it possible to exchange data structures between Lua and R and to execute arbitrary R programs directly from Lua.

Example code snippet:

```lua
local R = require "rclient"

local r = R.connect() -- Connect to a local R session.

-- Lua --> R (arrays):
r.v = { 1,2,3 }

-- Execute commands on the r session:
r "v <- v^2" --  Square v.
r "v"        --> [1] 1 4 9

-- R --> Lua (arrays):
local vb = r.v
print(vb[1], vb[2], vb[3]) --> 1, 4, 9

-- Lua --> R (others):
r.mymat  = R.asmatrix({ {1,2,3},{4,5,6} })
r.mylist = R.aslist({ 7,8,9 }, { "a","b","c" })
r.mydf   = R.asdataframe({ 7,8,9 }, { "a","b","c" }, { "row1" })

-- R --> Lua (others):
local arr2d = R.to2darray(r.mymat)  --  Array of arrays.
local map   = R.tomap(r.mylist)     --  Indexing via column names.
print(unpack(arr2d[1]))             --> 1, 2, 3
print(unpack(arr2d[2]))             --> 4, 5, 6
print(map.a[1], map.b[1], map.c[1]) --> 7, 8, 9
```

The Rclient library is part of the <a href="http://www.scilua.org">SciLua</a> framework which aims to offer a framework for numerical computing which combines the ease of use of scripting languages (Matlab, R, ...) with the high performance of compiled languages (C/C++, Fortran, ...). Please refer to the project's homepage for more information.
