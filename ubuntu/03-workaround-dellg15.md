## 临时解决DellG15 5520在Ubuntu上锁60Hz的问题
**注：此repo的EDID文件只适用于[RTX3060, 165Hz](https://item.jd.com/100032768490.html#crumb-wrap)的机型，240Hz及其他显卡型号的机型请看[其他型号](#其他型号)**
**应用此解决方案后将锁定屏幕到1920x1080@165Hz上，更改分辨率会直接黑屏**

### RTX3060 165Hz型号
1. 复制[EDID文件](./resources/edid.bin)到`/lib/firmware/edid`中，如果没有edid文件夹则创建一个
    * 创建`/lib/firmware/edid`需要超级用户(root)权限
2. 编辑`/etc/default/grub`，在`GRUB_CMDLINE_LINUX_DEFAULT`的`splash`后面加上`drm.edid_firmware=eDP-1:edid/edid.bin`
3. 执行`sudo update-grub`
4. 重启后应该就是165Hz模式了
    * 如果重启后不是，试试看`echo options i915 enable_fbc=1 | sudo tee /etc/modprobe.d/i915.conf`再重启

### 其他型号
1. 运行[这个脚本](./resources/get-edid)来获取你显示器的EDID文件
2. 然后用Wine运行[这个EDID编辑器](https://www.analogway.com/americas/products/software-tools/aw-edid-editor/)
    * [直链](https://www.analogway.com/files/uploads/produit/download/en/aw_edideditor_setup_2_00_13_windows.zip)
    * 下载解压好之后`wine <你EDID编辑器安装器exe的位置>`
3. 用编辑器打开你获取的EDID文件(建议在CurrentEdid.bin的位置打开终端用`cp ./CurrentEdid.bin ${WINEPREFIX:-$HOME/.wine}/drive_c`下面，这样在打开对话框里找C盘就能看见了)
4. 在`Detailed Data`栏点`CVT 1.2 Wizard`
5. 刷新率那里填`165.00`，然后保存文件
6. 接着根据[上面的过程](#rtx3060-165hz型号)复制文件、更新GRUB
7. 重启试试

方法来源：[StackExchange](https://unix.stackexchange.com/questions/680356/i915-driver-stuck-at-40hz-on-165hz-screen)

*问题能出现从本质上说还是Intel的集显驱动有问题*