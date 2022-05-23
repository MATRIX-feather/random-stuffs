修复ALG没有合盖睡眠的问题：
1. 编辑`/etc/systemd/logind.conf`
    1. 在这些条目前面加上"#"注释掉
        * `HandleSuspendKey=ignore`
        * `HandleHibernateKey=ignore`
        * `HandleLidSwitch=ignore`
2. 编辑`/etc/systemd/logind.conf.d/do-not-suspend.conf`
    1. 注释所有内容
3. 重启systemd-logind或者(建议)机器看看效果
    * 在我的ALG上面重启完systemd-logind之后总是会卡在进用户的阶段（登录完黑屏），需要切tty手动结束自己原有的gdm-x-session才行。
    * 重启systemd-logind.service的指令是`sudo systemctl restart systemd-logind.service`