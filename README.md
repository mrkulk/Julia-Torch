# Julia-Torch Summary
Interface between Julia and Torch (Lua) using ZMQ.

### Description
This module can be used to call torch functions from Julia. Currently the return values are restricted to be 1-D arrays but this can be easily changed in torch_server. Most importantly, since the torch server loads lua scripts, lua variables are persistent across multiple API calls. This is useful for instance when loading neural network models in torch once and asking it to return feature vectors across multiple batches.

### Usage
1. Start the torch ZMQ server by typing: 
```lua
th torch_server.lua
OR
luajit torch_server.lua
```
2. In your julia script, torch functions can now be accessed by:
```Julia
include("torch_interface.jl")
using TORCH
```
```Julia
#include all the required torch external scripts needed
script_names = 'test.lua'
TORCH.load_torch_script(script_names)
```
```Julia
#Call any function within scope of torch
func = "get_samples"
args = 1
TORCH.call(func, args)
```
