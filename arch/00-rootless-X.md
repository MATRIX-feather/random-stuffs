实现无root Xorg：

如果你的GNOME死活没法在Intel集显上跑[Rootless Xorg](https://wiki.archlinux.org/title/xorg#Rootless_Xorg)，试试看手动为i915启用modeset并配置Xwrapper

```Bash
echo "options i915 modeset=1" | sudo tee /etc/modprobe.d/intel-modeset.conf

echo "need_root_rights = no" | sudo tee /etc/X11/Xwrapper.config
```

执行完后重启登录执行`ps -o user $(pgrep Xorg)`，成功实现无root Xorg后输出应该和下面类似：
```
USER
<你的用户名>
```

如果你在设置完modeset和Xwrapper重启后发现进不去登录界面，那就重启到单用户模式把设置改回来吧...

在Grub界面编辑你的Arch启动项，在`linux..`最后面加上`single`，然后按[F10]引导，输入root密码登录后执行`rm /etc/X11/Xwrapper.config`和`rm /etc/modprobe.d/intel-modeset.conf`回退操作，完成后执行`exit`退出单用户模式。
