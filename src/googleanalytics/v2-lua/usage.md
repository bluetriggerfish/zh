### 修改 `AppDelegate.cpp`
* 修改 `Classes/AppDelegate.cpp` 文件，包含下列头文件：
```cpp
#include "PluginGoogleAnalyticsLua.hpp"
#include "PLuginGoogleAnalyticsLuaHelper.h"
```

* 然后，我们需要通过调用 `register_all_PluginGoogleAnalyticsLua(<lua_State*>);` 注册插件的 Lua\_State。

  __Note:__ 需要特别注意的是，该函数调用必须在 `lua_State *tolua_s = pStack->getLuaState();` 之后，并且在 `tolua_extensions_ccb_open(tolua_s);` 之前。

    这里为您准备了一个例子如下：
```cpp
#include "PluginGoogleAnalyticsLua.hpp"
#include "PluginGoogleAnalyticsLuaHelper.h"
bool AppDelegate::applicationDidFinishLaunching()
{
	lua_State *tolua_s = pStack->getLuaState();
	register_all_PluginGoogleAnalyticsLua(tolua_s);
	register_all_PluginGoogleAnalyticsLua_helper(tolua_s);
	tolua_extensions_ccb_open(tolua_s);
}
```

### 初始化 Google Analytics
修改您的 Lua 代码， 调用 `init()` 初始化插件。初始化可以放在代码的任何位置，但是，必须在使用插件功能之前完成。
```lua
sdkbox.PluginGoogleAnalytics:init()
```
