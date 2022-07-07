平常喜欢用的软件：
* `fcitx5-rime`
    * 搜狗拼音替代品
        * **强烈推荐搭配[四叶草方案](https://github.com/fkxxyz/rime-cloverpinyin)**
            * **也可以来试试我fork的自用分支qwq -> [MATRIX-feather/rime-cloverpinyin](https://github.com/MATRIX-feather/rime-cloverpinyin)**
        * 通过`sudo pacman -S fcitx5-rime fcitx5-gtk fcitx5-qt`安装
            * qt不知道是不是跟随rime自动安装，但gtk肯定不是，我一开始甚至为了这个上网搜半小时
    * 搜狗拼音**之前**在Ubuntu上和其他fcitx上的输入法有冲突（百度、讯飞等，19、20年那会Ubuntu上这三家只能同时装一个），如果你想在现在的arch上尝试一下，可以从AUR上获取：`sudo <yay或paru> -S fcitx-sogoupinyin`
        * 因为搜狗基于fcitx**4**，安装搜狗拼音将一并卸载fcitx5-rime

* `preload`
    * 会加快常用软件的加载速度
        * 具体介绍请参考[这里](https://wiki.archlinux.org/title/Preload_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#preload)
        * *不过实际用起来好像都差不多？*

* `linux-zen 或 linux-xanmod`
    * 一些第三方的Linux内核
        * 一般来说这些第三方内核*应该*会调教得更好些，但默认内核也够用，具体看需求，详见[ArchWiki - Kernel（简体中文）](https://wiki.archlinux.org/title/Kernel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
        * **如果你安装了第三方内核，请同样把`nvidia-dkms`装上，源里的`nvidia`和Ubuntu的一样，是给默认内核准备的**
        * xanmod内核需要[添加archlinuxcn源](./00-after-install.md#添加archlinuxcn源)

* `pavucontrol`
    * Pulseaudio音量调整，调起来比GNOME自带的体验好不少

* `netease-cloud-music 和 netease-cloud-music-gtk`
    * 网易云音乐客户端，前者是官方版本，后者是社区的GTK版本。平时单纯听歌可以用GTK，但求稳的话还是用官方版本吧...

* `pamac`
    * Arch包管理器pacman的GUI前端，用起来比CLI方便不少，AUR支持需要在首选项的第三方里打开
    * 就是搜索用起来有点卡

* `lutris 和 steam`
    * steam应该是Linux上最大的游戏平台了吧，steam上没有的可以在lutris上碰碰运气，比方说基岩版MC
        * 如果你发现PS5手柄在不支持自定义映射的wine游戏上怎么调都调不好，装上steam重启试试
        * 通过steam跑的游戏应该不会有什么映射问题，但如果使用lutris跑的，打开容器的注册表设置，将`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\winebus`中的`Enable SDL`设置成0，没有的话创建一个DWORD再设置就行

* `chrome-gnome-shell`
    * 浏览器上的GNOME插件管理集成

* `(AUR) deepin-wine-qq`
    * Wine QQ
        * 设置分辨率缩放：
            ```Bash
            export WINEPREFIX=~/.deepinwine/Deepin-QQ
            deepin-wine5 winecfg
            ```
            在打开的Wine设置里找到“显示”，将下方屏幕分辨率的dpi改到你想要的缩放，比方说1080p上125dpi会比默认的96好很多

* `(AUR) wps-office-cn`
    * WPS办公套件，它和libreoffice留一个就行。

* `(AUR) opentabletdriver`
    * 第三方数位板驱动，比内核的wacom驱动功能要多，最主要是能调映射，再也不用硬着头皮用100%全板健身辣
        * ~~[因为换成80%的全板了](../ubuntu/otd.json)~~

* `(AUR) system76-scheduler`
    * System76开发的CPU调度调优，配合[GNOME插件](https://extensions.gnome.org/extension/4854/system76-scheduler/)或[KDE的KWin脚本](https://store.kde.org/p/1789957)可以为前台应用给与更高优先级。
    * 同样也会为其他的一些程序（例如你的桌面或者系统的音频服务）优先调度
    * ~~System76 yyds~~

* `(AUR) visual-studio-code-bin`
    * VS Code

* `(外部) mcpelauncher`
    * MC基岩版安卓端启动器，可以通过[GitHub](https://github.com/ChristopherHX/linux-packaging-scripts/releases)获取
    * AUR上输`mcpe`也能搜到，但上次更新好像已经是去年了

GNOME插件：
* [`AppIndicator and KStatusNotifierItem Support`](https://extensions.gnome.org/extension/615/appindicator-support/)
    * 托盘支持

* [`Avatar`](https://extensions.gnome.org/extension/4782/avatar/)
    * 在系统目录显示你的头像

* [`Blur my Shell`](https://extensions.gnome.org/extension/3193/blur-my-shell/)

* [`Desktop Icons NG`](https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/)
    * 拒绝GNOME自带的桌面右键菜单
    * 但在GNOME自带的窗口截图中会显示一个透明的空窗口，看上去不大爽快。

* [`GSConnect`](https://extensions.gnome.org/extension/1319/gsconnect/)
    * KDE Connect的第三方GNOME适配，需要搭配手机端APP食用
    * **用防火墙的话需要开放1716～1764的TCP和UDP端口**

* [`Input Method Panel`](https://extensions.gnome.org/extension/261/kimpanel/)
    * 将fcitx输入面板像ibus那样集成到GNOME中，**强烈推荐！**

* [`Unite`](https://extensions.gnome.org/extension/1287/unite/)
    * 一些对GNOME的调整，还挺有用的。

* [`Just Perfection`](https://extensions.gnome.org/extension/3843/just-perfection/)
    * 同上

* [`System Action - Hibernate`](https://extensions.gnome.org/extension/3814/system-action-hibernate/)
    * 向GNOME电源菜单添加休眠选项
    * **休眠前记得检查你的内核启动参数，别忘了加resume。**
    * **详细信息可以在[这里](https://wiki.archlinux.org/title/Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Suspend_and_hibernate_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E4%BC%91%E7%9C%A0)找到**