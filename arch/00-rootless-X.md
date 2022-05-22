实现无root Xorg：

如果你的GNOME死活没法在Intel集显上跑[Rootless Xorg](https://wiki.archlinux.org/title/xorg#Rootless_Xorg)，试试看手动为i915启用modeset并配置Xwrapper

```Bash
sudo echo "options i915 modeset=1" >> /etc/modprobe.d/intel-modeset.conf

sudo echo "need_root_rights = no" >> /etc/X11/Xwrapper.config
```

执行完后重启登录执行`ps -o user $(pgrep Xorg)`，成功实现无root Xorg后输出应该和下面类似：
```
USER
<你的用户名>
```