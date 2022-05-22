更换Grub主题：
1. 复制主题到`/usr/share/grub/themes`中
2. 编辑`/etc/default/grub`
3. 找到`GRUB_BACKGROUND`
4. 注释掉这行，取消下面`GRUB_THEME`的注释
5. 将GRUB_THEME的值设置为你主题的theme.txt位置，例如`/usr/share/grub/themes/<主题>/theme.txt`
6. 更新GRUB
    * 如果配置生效，你会看到“找到主题：...”的提示

例如，如果要更换到此repo中的grub主题，你可以：
```Bash
#前往上级目录
cd ..

#复制主题
sudo cp ./assets/grub-theme-vimix /usr/theme/grub/themes -R

#编辑grub配置
sudo vim /etc/default/gurb

#在双引号里填你grub.cfg的位置，不填默认/boot/grub/grub.cfg
export GRUB_CFG=""

#更新GRUB配置
sudo grub-mkconfig -o "${GRUB_CFG:-/boot/grub/grub.cfg}"
```