## 电源管理：休眠
首先，你需要一个至少和内存一样大的swap分区。

然后：

1. 设置启动参数
    1. 打开你的磁盘管理工具，找到你swap分区的UUID。
    2. 编辑`/etc/default/grub`，找到`GRUB_CMDLINE_LINUX_DEFAULT`，在`quiet splash`后面加上`resume=UUID=<你swap分区的UUID>`
    3. 通过`grub-mkconfig -o /boot/grub/grub.cfg`更新grub配置

2. 配置initramfs钩子
    * **如果你根据[01-graphical-boot](./01-graphical-boot.md)配置了全图形化启动，那你不需要这步**
    1. 编辑`/etc/mkinitcpio.conf`，往下找到`HOOKS=`
    2. 在`base udev`后面加上`systemd`
        * 如果有`systemd`就不用加了
    3. 通过`mkinitcpio -P`更新当前initramfs

3. 重启再休眠试试

EX：挂起一段时间后休眠

1. 编辑`/etc/systemd/sleep.conf`
2. 去除`HibernateDelaySec`前面的注释
3. 将后面的值保留默认或改为你想要的时间就行
    * 默认值应该是2、3小时

* 不建议设置休眠到交换文件，如果你仍然想这么做，请参考[这里](https://wiki.archlinux.org/title/Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Suspend_and_hibernate_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E4%BC%91%E7%9C%A0%E5%88%B0%E4%BA%A4%E6%8D%A2%E6%96%87%E4%BB%B6)