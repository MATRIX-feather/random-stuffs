# 脚本
* nvrun: 为应用程序激活NVIDIA Offload
    * 用法: `nvrun <程序>`
* reload_nvidia: 重载NVIDIA闭源驱动，会注销当前会话
    * 用法：`reload_nvidia`
    * **只在Ubuntu 21.10上测试过**
* zinkrun: 通过zink运行OGL程序，不支持和NVIDIA闭源驱动搭配使用
    * 用法：`zinkrun <程序>`
    * **只在Ubuntu 21.10上测试过**