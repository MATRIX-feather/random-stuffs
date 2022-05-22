实现全程图形化启动：

1. 配置Plymouth
    1. 首先安装plymouth、gdm-plymouth
        * gdm-plymouth在安装时会提示和原有的gdm(gdm、libgdm)冲突，选择卸载原有的gdm即可，不会影响到现有的会话。~~除非你这时候gdm刚好崩了或者你选择重启GNOME~~
    2. 执行`sudo plymouth-set-default-theme bgrt`切换到BGRT主题
    3. 打开`/etc/mkinitcpio.conf`，找到“HOOKS”
    4. 在“base udev”后面加上`systemd sd-plymouth`,完成后HOOKS列表应该像这样：`... base udev systemd sd-plymouth ...`
    5. 执行`sudo mkinitcpio -P`更新当前initramfs
2. 配置系统（内核）启动参数
    1. 打开`/etc/default/grub`，找到`GRUB_CMDLINE_LINUX_DEFAULT`
    2. 在"quiet"后面加`splash`来让plymouth可以在启动时显示出来
        * 也许可以再加个`vt.handoff=7`，但我实测没啥变化或者变化不明显，懒得再去测了（
    3. 执行`sudo grub-mkconfig -o <你的GRUB配置文件地址>`
        * *一般来说，GRUB配置文件地址应该在`/boot/grub/grub.cfg`*
3. 重启看看效果