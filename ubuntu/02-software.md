软件推荐：
* `synaptic`
    * 图形化包管理
    * 通过`sudo apt install syanptic`安装

* `linux-oem`
    * Ubuntu官方的OEM内核，建议在有[Ubuntu认证](https://ubuntu.com/certified)的机器上安装，版本比默认的Generic/Lowlatency要高一些
    * **最主要是5.17(5.16)内核后合并了fsync，不用为这个单独装第三方内核了**
    * **并且源里有现成构建好的NVIDIA组件，不需要nvidia-dkms了**

* `现成的二进制NVIDIA组件`
    * 组件的包名应该是 `linux-modules-nvidia-<驱动版本>-<对应内核>-<Ubuntu版本?>`
        * 例如22.04上OEM内核的510版本就是`linux-modules-nvidia-510-oem-22.04`
    * 优点
        * 装上这个之后就不用每次更新内核都要等nvidia-dkms花时间自动重构NVIDIA驱动了
        * 基本上官方源里的内核都能找到对应的包
    * 缺点
        * 如果你用的第三方内核没提供他们自己构建的NVIDIA组件，那你还是得要装nvidia-dkms
        * 安装好后好像默认不自带？
        * 更新驱动大版本可能需要手动装一遍

* `deepin-wine.i-m.dev`
    * 移植Deepin-wine到Ubuntu上
    * 可以去看看他们的官网介绍：https://deepin-wine.i-m.dev/
        * QQ、微信、钉钉之类的都可以在上面找到

* WPS
    * 可能是Linux下最好的办公套件了，有官方支持
    * 国产之光（确信）
    * https://platform.wps.cn/

* VSCode
    * PC端跨平台编辑器，有官方Ubuntu支持
    * https://code.visualstudio.com/

* System76 Scheduler
    * 并没有
    * 在Issue上看到有人做了PPA：https://launchpad.net/~maxiberta/+archive/ubuntu/system76-scheduler
        * 添加PPA并安装：
            * **注：PPA和Arch的AUR差不多，请小心行事**
            ```Bash
                sudo add-apt-repository ppa:maxiberta/system76-scheduler
                sudo apt update
                sudo apt install system76-scheduler
            ```
    * 如果你不信任PPA，那么可以根据他们[官方目前给出的方法](https://github.com/pop-os/system76-scheduler/issues/40#issuecomment-1122848147)来安装，同样都是最终用包管理器装到系统上。

