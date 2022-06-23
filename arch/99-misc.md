## 杂项

### 默认用pinentry-gnome3作为pinentry界面
可以改进相关界面的集成度。
1. 编辑`~/.gnupg/gpg-agent.conf`
2. 添加`pinentry-program /usr/bin/pinentry-gnome3`
3. 执行`gpg-connect-agent reloadagent /bye`

### Chromium使用Vaapi

**注：此方案未经验证**

~~我chromium打开了一堆实验性的flag，全禁用再测试我怕找不回来~~

1. 编辑`/usr/share/applications/chromium.desktop`
    1. 在所有`Exec = chromium %U`后面加上`-enable-features=VaapiVideoEncoder,VaapiVideoDecoder --disable-features=UseChromeOSDirectVideoDecoder --enable-accelerated-video-decode`
    * 把/usr/share下面的chromium.desktop复制到`~/.local/share/applications`里再编辑也行，而且不需要root就能改，但不知道为什么在Ubuntu上没事，在ALG上就丢MIME了

此方案同样对Chrome也同样适用

### 修复Chromium在部分Intel集显上启动报“libva error: /usr/lib/dri/i965_drv_video.so init failed”

* 安装`intel-media-driver`
    * `sudo pacman -S intel-media-driver`
    * 这个装上之后就可以卸掉`libva-intel-driver`了，因为很明显你并不需要i915_drv_video.so，你需要的是iHD，留着i915反而可能会让一些程序用错误的库。

### Intel集显相关

1. 先通过`sudo pacman -S intel-gpu-tools`安装相关工具
2. 执行`sudo intel_gpu_frequency`看看当前集显工作频率(`cur: ...`)
3. 安装完成后执行`sudo intel_gpu_frequency -m`将集显最低频率拉满
4. 再`sudo intel_gpu_frequency`看看效果
* 实测可以极大缓解GNOME的卡顿问题

### 内核组件黑名单
* 可以试试将[modprobe_blacklist](./modprobe_blacklists/)里的所有conf复制到`/etc/modprobe.d/`下面
    * 这些是我从Ubuntu 21.10备份里取到的，可以加上看看。
    * 比方说[blacklist.conf](./modprobe_blacklists//blacklist.conf)里的`blacklist pcspkr`就可以防止主板在你关机/重启/休眠时突然响一声~~助力你的心脏病发展~~吓你一跳

### Xorg配置文件
* 可以试试将[xorg.conf.d](./xorg.conf.d/)里的所有conf复制到`/usr/share/X11/xorg.conf.d`中
    * 同样是我从Ubuntu 21.10备份里取到的，可能会对你有所帮助。
    * `10-nvidia.conf`中我把`ModulePath`的路径给改了改，避免复制到Arch后会找不到相关文件

### (AUR) mutter-performance
* 据说可以优化GNOME窗管的性能，感觉确实有一点改进
* 可以通过当前系统管理AUR的程序安装
    * 例如：`sudo <paru或yay> -S mutter-performance`
* **注1: 不建议i+N显卡用户使用，三重缓冲补丁在一些OGL游戏上（例如osu!lazer）全屏会有卡死的问题，只能进tty重启GNOME**
    * 好像三重缓冲补丁打上之后所有原生SDL程序全屏都会出问题，暂时可以[通过插件禁用全屏undirect](https://extensions.gnome.org/extension/4509/disable-unredirect-fullscreen-windows/)缓解，但代价是在视觉上会有延迟(在我这60Hz的屏幕上很明显)，如果想用这个缓解办法打osu这种对延迟很敏感的游戏的话，还是换回原版mutter吧...
    * 三重缓冲补丁可以用yay通过`yay --editmenu -S mutter-performance`的方式编辑PKGBUILD来禁用补丁
        1. 在“要编辑哪些PKGBUILDs？”处选中mutter-performance
        2. 在`_merge_requests_to_use=('1441' '1877')`那里移除1441
        3. 保存并退出
            * vim的退出方式是按`ESC`+`:`+`wq`+`ENTER`
            * nano用`CTRL`+`X`，然后根据提示保存即可
        4. 继续安装
* **注2：此包依赖的wireplumber会破坏原有的pulseaudio，如果重启后没有声音，请安装`pipewire-pulse`**
    * 也可以用`sudo pacman -S mutter`重装回默认的mutter，但wireplumber不一定会跟着卸载，具体怎么装回pulseaudio我暂时还没头绪，或许可以参考一下[这个文档](https://www.archlinuxcn.org/undone-replacement-of-pipewire-media-session-with-wireplumber/)？

### ALSOFT实时音频相关
* 能解决Minecraft报错`[ALSOFT] (EE) Failed to set real-time priority for thread: 不允许的操作(1)`
* ***可能****会与system76-scheduler冲突，因为两个都和设置进程优先级有关*
* 安装`realtime-privileges`，然后`sudo usermod -G realtime -a $(whoami)`
* 配置完成后重启再试试

### NVIDIA驱动调教
#### 启用PAT
根据[Arch wiki](https://wiki.archlinux.org/title/NVIDIA/Tips_and_tricks#Kernel_module_parameters)上的描述，启用PAT似乎可以改善性能

编辑`/etc/modprobe.d/nvidia-pat.conf`或`/lib/modprobe.d/nvidia-pat.conf`，输入以下内容：
```
options nvidia "NVreg_UsePageAttributeTable=1"

#你可能也需要手动启用N卡的KMS
options nvidia-drm modeset=1
```
完成后重启看看效果

~~老实说我感觉效果不大，不管是MC还是原神开垂直同步的情况下GPU占用一点没少~~