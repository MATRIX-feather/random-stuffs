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

### (AUR) mutter-performance
* 据说可以优化GNOME窗管的性能，感觉确实有一点改进
* 可以通过当前系统管理AUR的程序安装
    * 例如：`sudo <paru或yay> -S mutter-performance`
* **注1: 不建议i+N显卡用户使用，三重缓冲补丁在一些OGL游戏上（例如osu!lazer）全屏会有卡死的问题，只能进tty重启GNOME**
* **注2：此包依赖的wireplumber会破坏原有的pulseaudio，如果重启后没有声音，请安装`pipewire-pulse`**
    * 也可以用`sudo pacman -S mutter`重装回默认的mutter，但wireplumber不一定会跟着卸载，具体怎么装回pulseaudio我暂时还没头绪，或许可以参考一下[这个文档](https://www.archlinuxcn.org/undone-replacement-of-pipewire-media-session-with-wireplumber/)？