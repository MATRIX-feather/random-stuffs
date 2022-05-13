# 脚本
* nvrun: 为应用程序激活NVIDIA Offload
    * 用法: `nvrun <程序>`
* reload_nvidia: 重载NVIDIA闭源驱动，会注销当前会话
    * 用法：`reload_nvidia`
    * **只在Ubuntu 21.10上测试过**
* zinkrun: 通过zink运行OGL程序，不支持和NVIDIA闭源驱动搭配使用
    * 用法：`zinkrun <程序>`
    * **只在Ubuntu 21.10上测试过**
* x11_force_release: 防止有捕获光标的大聪明无响应之后让整个X11会话没光标用
    * 需要xdotool，*可能*会降低相关安全性
        * ~~不过要真有恶意程序要模拟键鼠一般都会自备相关的库吧~~