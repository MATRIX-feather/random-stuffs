### 保留我现在的内核模块！
[添加archlinuxcn源](./00-after-install.md#导入archlinuxcn)后安装`kernel-modules-hook`，可以避免pacman在更新内核时把当前内核的模块扬了导致你必须重启不然得一直提心吊胆地用系统

### 不要在关机的时候卸载所有文件系统
* 可以避免关机关到最后刷`... /oldroot ... Device is busy`
        * 不是非常必要
1. 执行`sudo systemctl mask mkinitcpio-generate-shutdown-ramfs.service`

### 换主题
ALG安装好之后应该是会自动换到Orchis主题的，但如果没有：
        1. 打开“优化”（gnome-tweaks）
        2. 在“外观”栏找到“过时应用程序”和“Shell”
        3. 点开他们旁边的下拉菜单，选择`Orchis-<你喜欢的颜色>`

### 字体
默认字体对我来说有点小，所以我一般会把大小调到13号

### 本地PATH
本地PATH可以更方便地储存可执行文件，对于那些只会在自己系统帐号里用上的程序就不用大费力气上sudo搁 /usr/local 里了。

~~具体是怎么做的我也忘记了，所以这小节的内容可能不大准~~

1. 可能的方案A：
    1. 打开`~/.bash_profile`
    2. 在第一行添加`export PATH="${PATH}:${HOME}/.local/bin"`
    3. 注销重进或者重启看看
    * 这应该是我从Ubuntu转到Arch前原有的方案，不知道在Arch下是怎么生效的，但".local/bin"稳定在PATH的最后面
2. 经过测试的方案B：
    1. 创建`~/.config/environment.d/path.conf`
    2. 向里面写入`PATH=${PATH}:${HOME}/.local/bin`
    * 在全新安装的home上可以稳定生效，但".local/bin"好像不在PATH的最后面

### 用zstd压缩initramfs以优化开机速度
1. 编辑`/etc/mkinitcpio.conf`
2. 注释掉`COMPRESSION="xz"`
3. 取消`COMPRESSION="zstd"`前面的注释
4. 执行`sudo mkinitcpio -P`更新initramfs