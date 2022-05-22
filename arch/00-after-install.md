安装完成后的操作：

1. 卸载reflector
    1. 打开终端，执行`sudo pacman -R reflector`
    2. 这样可以避免reflector老是覆盖pacman镜像源

2. 安装CJK字体和防火墙
    ```Bash
    #防火墙
    sudo pacman -S gufw noto-fonts-cjk

    #配置防火墙
    sudo gufw
    ```
    将“状态”旁的开关点开就行

3. 安装一些必要软件

4. 导入archlinuxcn
    * [https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/)

    * 快捷应用
        ```Bash
        #根据介绍导入源
        sudo echo "[archlinuxcn]
        Server = https://repo.archlinuxcn.org/\$arch" >> /etc/pacman.conf

        #更新列表
        sudo pacman -Sy

        #导入他们的GPG key和镜像表
        sudo pacman -S archlinuxcn-keyring archlinuxcn-mirrorlist-git
        ```

    * `archlinuxcn-mirrorlist-git`在安装后，`/etc/pacman.d/`下面应该会多一个"archlinuxcn-mirrorlist"，使用`sudo nano /etc/pacman.d/archlinuxcn-mirrorlist`，挑选一个镜像源，删掉前面的“#”，然后 [Ctrl]+[X] -> [y] -> [回车] 保存后通过`sudo pacman -Sy`更新源即可。
5. 换主题
    * ALG安装好之后应该是会自动换到Orchis主题的，但如果没换到：
        1. 打开“优化”（gnome-tweaks）
        2. 在“外观”栏找到“过时应用程序”和“Shell”
        3. 点开他们旁边的下拉菜单，选择`Orchis-<你喜欢的颜色>`
6. 字体
    * 默认字体对我来说有点小，所以我一般会把大小调到13号
7. 本地PATH
    * 本地PATH可以方便
    * ~~具体是怎么做的我也忘记了，所以这小节的内容可能不大准~~
    1. 可能的方案A：
        1. 打开`~/.bash_profile`
        2. 在第一行添加`export PATH="${PATH}:${HOME}/.local/bin"`
        3. 注销重进或者重启看看
        * 这应该是我从Ubuntu转到Arch前原有的方案，不知道在Arch下是怎么生效的，但".local/bin"稳定在PATH的最后面
    2. 经过测试的方案B：
        1. 创建`~/.config/environment.d/path.conf`
        2. 向里面写入`PATH=${PATH}:${HOME}/.local/bin`
        * 在全新安装的home上可以稳定生效，但".local/bin"好像不在PATH的最后面
8. 用zstd压缩initramfs以优化开机速度
    1. 编辑`/etc/mkinitcpio.conf`
    2. 注释掉`COMPRESSION="xz"`
    3. 取消`COMPRESSION="zstd"`前面的注释
    4. 执行`sudo mkinitcpio -P`更新initramfs