## 修复网易云音乐无法启动
* *方法截至2022年7月7日仍然有效，如果哪次更新突然爆炸了我会在找到方法之后回来更新这里*
1. 复制[netease-cloud-music](./resources/netease-cloud-music/)下面的两个库到`/opt/netease-cloud-music/libs`下面，启动看看
    * 在`resources/netease-cloud-music`中打开终端执行以下指令：
        ```Bash
            sudo cp ./* /opt/netease-cloud-music/libs/
        ```