## 安装完成后的操作

### 卸载reflector
*目前对我没有什么用，所以我在这里选择卸载*
1. 打开终端，执行`sudo pacman -R reflector`
2. 这样可以避免reflector老是覆盖pacman镜像源
* reflector配置好的话也可以自动刷新成国内源，但我目前不大需要

### 换源
1. 编辑`/etc/pacman.d/mirrorlist/`
    1. 在第一行Server上面插入`Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch`更换到清华源
    * 也可以更换成国内其他地方的镜像源，我这里用清华源速度会更快点

### 添加archlinuxcn源
* [官网介绍](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/)

* 快捷应用
    ```Bash
    #根据介绍导入源
    echo "[archlinuxcn]
    Server = https://repo.archlinuxcn.org/\$arch" | sudo tee -a /etc/pacman.conf

    #更新列表
    sudo pacman -Sy

    #导入他们的GPG key和镜像表
    sudo pacman -S archlinuxcn-keyring archlinuxcn-mirrorlist-git
    ```

#### 为archlinuxcn更换国内镜像源
* *如果你那里cn源下载速度正常，那么可以选择跳过本节*
* `archlinuxcn-mirrorlist-git`在安装后，`/etc/pacman.d/`下面应该会多一个"archlinuxcn-mirrorlist"
* 使用`sudo nano /etc/pacman.d/archlinuxcn-mirrorlist`，挑选一个镜像源，删掉前面的“#”，然后 [Ctrl]+[X] -> [y] -> [Enter]保存退出
* 接着编辑`/etc/pacman.conf`，把cn源的`Server = ...`改成`Include = /etc/pacman.d/archlinuxcn-mirrorlist`
* 再使用`sudo pacman -Sy`更新看看速度

### 安装CJK字体和防火墙
```Bash
#防火墙
sudo pacman -S gufw noto-fonts-cjk

#配置防火墙
sudo gufw
```
将“状态”旁的开关点开就行

### 安装一些必要软件
* 可以参考[这个列表](./02-software.md)