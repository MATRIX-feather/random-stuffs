### 保留我现在的内核模块！
[添加archlinuxcn源](./00-after-install.md#导入archlinuxcn)后安装`kernel-modules-hook`，可以避免pacman在更新内核时把当前内核的模块扬了导致你必须重启不然得一直提心吊胆地用系统

### 不要在关机的时候卸载所有文件系统
* 可以避免关机关到最后刷`... /oldroot ... Device is busy`
        * 不是非常必要
1. 执行`sudo systemctl mask mkinitcpio-generate-shutdown-ramfs.service`

### 换主题
推荐[Vince](https://www.pling.com/u/vinceliuice/)大佬的全套主题。

~~主题好看 + 是国人 = 芜湖起飞~~
* Orchis
    * 可以在[pling](https://www.pling.com/p/1357889)或[GitHub](https://github.com/vinceliuice/Orchis-theme)上找到
    * *ALG*安装好后应该是自带Orchis的
* Graphite
    * 可以在[pling](https://www.pling.com/p/1598493)或[GitHub](https://github.com/vinceliuice/Graphite-gtk-theme)上找到
    * ~~每次一出新主题，上个主题马上就不香了~~
* Fluent
    * Windows风格的主题
    * 有两个变种：
        * [Fluent gtk theme](https://www.pling.com/p/1477941)：Win10风格
        * [Fluent round gtk theme](https://www.pling.com/p/1574551)：Win11风格
* 其他主题可以去他的Github或pling主页找找，向下翻到"GTK3/4 Themes"

另外这些主题也可以看看：
* Catppuccin
    * ~~猫布丁主题~~
    * 可以在[GitHub](https://github.com/catppuccin/catppuccin)上找到，下方的"[Ports and more!](https://github.com/catppuccin/catppuccin#-ports-and-more)"可以找到以适配的平台
    * 在AUR上可以搜到对应的GTK、Grub、SDDM主题和壁纸
    * **现役主题，用起来还算舒适**
    ![主题截图](https://s3.bmp.ovh/imgs/2022/05/30/a7cde2fd06d89637.png)
* Flat Remix
    * 可以在[pling](https://www.pling.com/p/1214931/)或[GitHub](https://github.com/daniruiz/Flat-Remix-GTK)上找到
    * 我接触的第一个自定义主题

至于怎么换主题：
1. 打开“优化”（gnome-tweaks）
2. 在“外观”栏找到“过时应用程序”和“Shell”
3. 点开他们旁边的下拉菜单，选择你想换的主题

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

### 允许免密码改打印机设置
方法来自[Arch Wiki](https://wiki.archlinux.org/title/CUPS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%85%81%E8%AE%B8%E9%80%9A%E8%BF%87_PolicyKit_%E8%BF%9B%E8%A1%8C%E7%AE%A1%E7%90%86%E5%91%98%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

编辑`/etc/polkit-1/rules.d/49-allow-passwordless-printer-admin.rules`，输入以下内容：
```
polkit.addRule(function(action, subject) { 
    if (action.id == "org.opensuse.cupspkhelper.mechanism.all-edit" && 
        subject.isInGroup("wheel")){ 
        return polkit.Result.YES; 
    }
});
```

PS: 在设置前，你需要先保证：
* `cups-pk-helper`有安装在系统上
    * ALG安装时已经帮你装好了
* 你自己在`wheel`组里
    * *你应该在安装的时候就已经分配好了，不然你怎么用的sudo（*