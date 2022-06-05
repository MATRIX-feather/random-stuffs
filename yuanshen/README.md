# yuanshen
和Wine原神有关的东西

## Wine版本建议
* [TKG](https://github.com/Frogging-Family/wine-tkg-git)：综合表现比较好，[而且有为目前的主流发行版提供安装包(Arch、Fedora、Ubuntu)](https://github.com/Frogging-Family/wine-tkg-git/actions)
    * Playstation手柄需要禁用SDL才能在游戏内显示正常。
    * PS5手柄必须禁用SDL，不然用都没法用。
        * *禁用SDL后请避免操作摇杆或扳机键的时候关闭手柄，不然游戏会一直保持关闭前的状态，直到下次启动*
        * 启用、禁用SDL的注册表项可以在[registries](./registries/)里找到，用容器的注册表编辑器导入即可。

* [GE-Proton](https://github.com/GloriousEggroll/wine-ge-custom/)：**游戏在桌面进概览时会严重掉帧(在GNOME上用Proton跑游戏都会这样)**，但目前只有GE不会在我电脑过热时在稻妻城内过度掉帧
    * **不需要禁用SDL就可以正常使用PS手柄**
    * 不建议在GNOME上直接开启全屏，可以先在游戏内开启全屏独占，然后`Alt+Enter`退出全屏，接着用`Alt+F11`进入全屏无边框。
        * *Alt+F11需要手动在**GNOME设置**中进入 键盘 -> 查看及自定义快捷键 -> 窗口 -> 切换全屏模式 配置。*
    * 游戏窗口可能会没有图标，重启GNOME后会显示
        * *讲真，真的会有人因为这个专门去重启GNOME吗？*

* 原版Wine：除非你真的没得选，不然我非常不建议用原版Wine跑游戏。

## DXVK
一般来讲和wine游戏有关的启动器都会自动为你配置好DXVK（比方说[Lutris](https://lutris.net/)和[Wine游戏助手](https://winegame.net/index.html?r=5)，国内建议优先选择Wine游戏助手，有梯子再用Lutris），但如果他们没有：
1. 前往DXVK的[release页面](https://github.com/doitsujin/dxvk/releases/latest)
2. 往下翻，下载`dxvk-xxx.tar.gz`
3. 解压下载到的压缩文件
4. 打开终端
5. 设置好你的Wine容器地址
    * `export WINEPREFIX=<你的Wine容器地址>`
6. 运行解压目录里的`setup_dxvk.sh`
    * 安装DXVK需要在脚本后面添加启动参数，添加后整条命令应该会像这样：`... setup_dxvk.sh install`
7. 启动游戏看看

判断有没有配置好DXVK的方法很简单：看画面，如果游戏画面很明显和其他平台不一样，那就是没装。

**PS: 你的游戏管理器/启动器可能会覆盖当前安装的DXVK，我建议在手动安装前先去找找相关设置，实在找不到再手动安装。**

## 性能优化
### ESync或FSync
添加环境变量`WINEESYNC=1`、`WINEFSYNC=1`、`WINEFSYNC_FUTEX2=1`可以让Wine根据你的内核自动启用FSync或ESync。

原版内核从5.16开始就集成了FSync，只需要你用的Wine有FSync补丁即可。可以参考上面的[Wine版本建议](#wine版本建议)，第三方内核可以尝试一下[xanmod](https://xanmod.org/)或[liquorix](https://liquorix.net/)。

esync和fsync开启时终端或日志会有提示，如：`fsync: up and running`

更多有关FSync和ESync的信息，可以参考一下[这里](https://github.com/AdelKS/LinuxGamingGuide#esync-fsync-futex2)

### DXVK设置
可以参考一下[我的DXVK设置](./dxvk.conf)

### 使用异步DXVK
异步DXVK可以在[这里找到](https://github.com/Sporif/dxvk-async/releases/tag/1.10.1)，安装方法和DXVK一样。

## 其他资源
* [dxvk.conf](./dxvk.conf): 我的dxvk配置文件
* [YuanShenLutrisCover.png](./YuanShenLutrisCover.png): 适用于Lutris的封面
    * 自己做的，不喜轻喷🙏
* [browserfix](./browserfix/): 解决Wine原神点不开部分公告链接的问题
* [watch_device_lost](./watch_device_lost/): 在DXVK报VK_ERROR_DEVICE_LOST时自动结束进程
    * 用launchall、closeall可以快捷启动、停止上述两个脚本
* [registries](./registries/)：注册表相关资源，目前用于启用、禁用winebus的SDL