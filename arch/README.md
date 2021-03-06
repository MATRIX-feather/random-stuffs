一些在Arch上折寿的笔记

PS：我目前的Arch是通过ALG安装到硬盘上，可能与CLI安装的情况有所不同。

*如果你第一次接触Linux桌面，我的建议是先从Ubuntu或Deepin开始，然后再去尝试别的发行版。*

## 已知问题
截至目前我在我这电脑上遇到了这些无法解决的问题：

### Arch（ALG？）独有
* 在睡眠、休眠后除非重启驱动，不然无法使用N卡来加速编、解码
* ~~Arch上的GNOME有内存溢出的问题~~ Ubuntu上也遇到了
* Arch上的GNOME默认文管(nautilus)会经常崩溃
* 就算启用了N卡的KMS，GNOME也不允许使用Wayland
    * *`/etc/gdm/custom.conf`中WaylandEnable是true*

## 目录
* 00 ) [安装后要做的事](./00-after-install.md)
    * [卸载reflector](./00-after-install.md#卸载reflector)
    * [换源](./00-after-install.md#换源)
    * [添加archlinuxcn源](./00-after-install.md#添加archlinuxcn源)
        * [为archlinuxcn更换国内镜像](./00-after-install.md#为archlinuxcn更换国内镜像源)
    * [安装字体和防火墙](./00-after-install.md#安装cjk字体和防火墙)
    * [禁用pcspkr](./00-after-install.md#禁用pcspkr)
    * [禁用root登录](./00-after-install.md#禁用root登录)
* 01 ) [做这些能让你的Arch体验更美好](./01-qol-changes.md)
    * [升级内核时保留现有的模块](./01-qol-changes.md#保留我现在的内核模块)
    * [解决关机时刷`... /oldroot ... Device is busy`](./01-qol-changes.md#不要在关机的时候卸载所有文件系统)
    * [换主题](./01-qol-changes.md#换主题)
    * [字体](./01-qol-changes.md#字体)
    * [本地PATH](./01-qol-changes.md#本地path)
    * [用zstd压缩initramfs以优化开机速度](./01-qol-changes.md#用zstd压缩initramfs以优化开机速度)
    * [允许免密改打印机设置](./01-qol-changes.md#允许免密码改打印机设置)
    * [用ntfs3挂载ntfs文件系统](./01-qol-changes.md#默认用内核的ntfs3来挂载ntfs文件系统)
    * [使nautilus可以为视频生成缩略图](./01-qol-changes.md#使nautilus可以为视频生成缩略图)
    * [避免自己被锁在自己账户外面](./01-qol-changes.md#避免自己被锁在自己账户外面)
* 02 ) [休眠](./01-hibernate.md)
* 03 ) [无特权X服务器](./01-rootless-X.md)
* 04 ) [全程图形化启动，避免无意义的输出](./01-graphical-boot.md)
* 05 ) [Grub主题](./01-grub-theme.md)
* 06 ) [软件推荐](./02-software.md)
* 07 ) [我需要合盖睡眠！](./03-i-need-auto-suspend.md)
* 08 ) [杂项](./99-misc.md)
    * [默认用pinentry-gnome3作为pinentry界面](./99-misc.md#默认用pinentry-gnome3作为pinentry界面)
    * [Chromium使用Vaapi](./99-misc.md#chromium使用vaapi)
    * [修复Chromium在部分Intel集显上启动报“libva error: /usr/lib/dri/i965_drv_video.so init failed”](./99-misc.md#修复chromium在部分intel集显上启动报libva-error-usrlibdrii965drvvideoso-init-failed)
    * [Intel集显相关](./99-misc.md#intel集显相关)
    * [内核组件黑名单](./99-misc.md#内核组件黑名单)
    * [Xorg配置文件](./99-misc.md#xorg配置文件)
    * [使用mutter-performance以优化GNOME的性能](./99-misc.md#aur-mutter-performance)
    * [ALSOFT实时音频相关](./99-misc.md#alsoft实时音频相关)