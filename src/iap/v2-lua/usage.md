### 修改 `AppDelegate.cpp`
* 修改 `Classes/AppDelegate.cpp` 包含如下文件:
```cpp
#include "PluginIAPLua.hpp"
#include "PluginIAPLuaHelper.h"
```

* 然后, 我们需要调用 `register_all_PluginIAPLua(<lua_State*>);` 来把插件注册到lua中.

  __注意:__ 一定要要保证上面的调用是在`lua_State *tolua_s = pStack->getLuaState();` 之后, 而且是在 `tolua_extensions_ccb_open(tolua_s);`.

	下面给出了一个例子:
```cpp
#include "PluginIAPLua.hpp"
#include "PluginIAPLuaHelper.h"
bool AppDelegate::applicationDidFinishLaunching()
{
	lua_State *tolua_s = pStack->getLuaState();
	register_all_PluginIAPLua(tolua_s);
	register_all_PluginIAPLua_helper(tolua_s);
	tolua_extensions_ccb_open(tolua_s);
}
```

### 初始化 IAP
修改您的lua代码去初始插件, 初始化可以在任何地方来做,但是必须要在您想使用插件的功能之前.
```lua
sdkbox.IAP:init()
```

### 获取最新的商品数据
最好在您的游戏开始前从服务器获取一次最新的商品数据

要获取商品数据,只需要简单调用 `sdkbox.IAP:refresh()`.

> `onProductRequestSuccess` 获取成功会收到这个事件.

> `onProductRequestFailure` 获取失败收到这个事件.

### 购买
购买商口调用 `sdkbox.IAP:purchase(name)`

__注意:__ __name__ 是您工程的 IAP 配置文件中的 `items` 项下的名字,而不是您在 iTunes 或 GooglePlay Store中的商品名

> `onSuccess` 购买成功事件.

> `onFailure` 购买失败事件.

> `onCanceled` 用户取消购买,会触发这个事件.

### 恢复购买
恢复购买调用 `sdkbox.IAP:restore()`.

> `onRestored` 恢复成功事件.

__注意:__ `onRestored` 可能被会多次触发

### 处理付费事件
您可以接收付费过程中的 `IAP` 事件, 不同事件对用户, IAP 服务器做不同的处理.
```lua
sdkbox.IAP:setListener(function(args)
		if "onSuccess" == args.event then
				local product = args.product
				dump(product, "onSuccess:")
		elseif "onFailure" == args.event then
				local product = args.product
				local msg = args.msg
				dump(product, "onFailure:")
				print("msg:", msg)
		elseif "onCanceled" == args.event then
				local product = args.product
				dump(product, "onCanceled:")
		elseif "onRestored" == args.event then
				local product = args.product
				dump(product, "onRestored:")
		elseif "onProductRequestSuccess" == args.event then
				local products = args.products
				dump(products, "onProductRequestSuccess:")
		elseif "onProductRequestFailure" == args.event then
				local msg = args.msg
				print("msg:", msg)
		else
				print("unknow event ", args.event)
		end
end)
```
