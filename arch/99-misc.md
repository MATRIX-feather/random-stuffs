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