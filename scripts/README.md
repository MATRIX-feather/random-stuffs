# 脚本
**这些脚本只在Ubuntu 22.04上测试运行过**
**~~一些黑历史/高血压脚本能用就不要深究了（~~**

* nvrun: 为应用程序激活NVIDIA Offload
    * 用法: `nvrun <程序>`
* reload_nvidia: 重载NVIDIA闭源驱动，会注销当前会话
    * 用法：`reload_nvidia`
* zinkrun: 通过zink运行OGL程序，不支持和NVIDIA闭源驱动搭配使用
    * 用法：`zinkrun <程序>`
* x11_force_release: 防止有捕获光标的大聪明无响应之后让整个X11会话没光标用
    * 用法：`x11_force_release`
    * 需要xdotool，*可能*会降低相关安全性
        * ~~不过要真有恶意程序要模拟键鼠一般都会自备相关的库吧~~
* exec-wrapper: 程序启动包装器，可以用来简化一些程序的启动过程
    * 例如你装有Graphite-Light主题，但你又向让Chrome用Graphite作为主题，那么你就可以用此脚本在chrome启动前设置