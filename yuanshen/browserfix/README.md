# 浏览器修复
修复原神无法在wine中启动系统浏览器

## 依赖 
脚本依赖以下组件或指令：

* Bash
* xdg-open(默认打开URL用的指令)
* inotify-tools(如果启用了inotify)

## 用法
1. 找到原神的Wine容器

2. 将xxdg-open链接到容器的`C:\windows`中并改名叫`xxdg-open.exe`

3. 打开容器的注册表编辑器，导入[xxdg.reg](xxdg.reg)，或者：
    1. 找到`HKEY_CLASSES_ROOT -> http -> shell -> open -> command`
    2. 将默认值设置为`xxdg-open.exe "%1"`
    3. 同理，找到`HKEY_CLASSES_ROOT -> https -> shell -> open -> command`并将其默认值设置为`xxdg-open.exe "%1"`

4. 在游戏启动前运行`startbrowserfix`脚本即可启动脚本

5. 启动游戏，随便点开一个登录界面公告里的链接看看（米游社、微博这些）

6. 游戏结束后，运行`endbrowserfix`结束脚本

## 自定义
* 多数自定义选项均在[common](common)中

* 将`USEINOTIFY`环境变量设置为`1`后脚本将通过inotifywait检测URL文件
    * 此方式相较于之前的loop方案对于cpu的负担要更小些
    * inotifywait命令的文件位置可以通过设置`INOTIFY`环境变量来调整，设置后脚本将尝试用变量中的可执行文件作为inotifywait执行

## 原理
通过xxdg-open将调用的URL写到指定的文件里再让browserfix读取并执行，可以避免通过wine调用导致继承环境变量之类的东西让浏览器出错(例如针对某一游戏配置的LD_PRELOAD、LD_LIBRARY_PATH)

~~省流：既然直接调用会出毛病，那不直接调用不就行了（~~