# deepin
## xanmod内核相关
### NVIDIA闭源驱动dkms报IGNORE_CC_MISMATCH
编辑`/usr/src/nvidia-current/conftest.sh`，在第9行`CC="$1"`前加上`IGNORE_CC_MISMATCH=1`

这样可以避免安装xanmod内核时源内nvidia dkms构建报内核CC和系统CC不一致导致不构建的问题

### UEngine
在这里打开终端，然后：

```Bash
#设置文件权限
chmod g-w xanmod-load-anbox-module/usr -R
chmod g-w xanmod-load-anbox-module/etc -R

sudo chown root:root xanmod-load-anbox-module/usr -R
sudo chown root:root xanmod-load-anbox-module/etc -R

#打成软件包
dpkg -b ./xanmod-load-anbox-module

#安装！
sudo apt install ./xanmod-load-anbox-module.deb
```

装完之后重启，应该就能使用安卓应用了

其他应该也适用于其他用systemd的Debian发行版