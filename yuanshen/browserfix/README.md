# 浏览器修复
修复原神无法在wine中启动系统浏览器

## 依赖 
脚本依赖以下组件或指令：

* Bash
* disown
* xdg-open(默认打开URL用的指令)

## 用法
1. 复链接xxdg-open到你的PATH中
    * 推荐位置:
        * `$HOME/.local/bin` (可能需要手动设置`PATH`变量才能使用)
            * 具体怎么设置我也不知道，忘记了(逃)
        * `/usr/local/bin` (可能需要root，除非你的发行版是SteamOS那种只读根目录或者有自己的想法)
        * `/usr/bin` 或 `/bin` (需要root，最方便，**但可能会导致维护困难**~~(例如“这个xxdg-open是哪个包里的？”)~~，除非你的发行版是SteamOS那种只读根目录或者有自己的想法)
    * 如何为原神自定义PATH？

        1. 首先我们假设你在用Lutris或者wine游戏助手，并且把xxdg-open存在了`/home/a8a8/browserfix`里

        2. 在终端中执行以下指令：
            ```Bash
            echo "这里替换成你存xxdg-open脚本的地方:$PATH"
            ```

        3. 然后你会得到类似于`...的地方:/usr/local/bin...`的输出

        4. 复制你的到的那段输出

        5. 打开Lutris或者wine游戏助手，选择原神，点启动右边的那个小三角

        6. 在打开的菜单里点“配置”

        7. 点击“系统选项”标签，往下拉找到“环境变量”

        8. 点击添加，然后点击第一栏(Key)，里面填`PATH`

        9. 然后点击第二栏(Value)，里面粘贴上你刚才复制的输出

        10. 将“这里替换成你存xxdg-open脚本的地方”替换成...你放xxdg-open脚本的地方，这个例子里是`/home/a8a8/browserfix` owo

        11. 保存
            * 其他管理器只要能设置环境变量应该都可以用此方法设置PATH
            * 终端、脚本用`export PATH=<复制的输出>`就行，请记得按照第10步替换相关文本

2. 在原神的Wine容器中打开注册表编辑器(regedit)

3. 找到`HKEY_CURRENT_USER -> Software -> Wine -> WineBrowser`

4. 将`Browsers`键的值改成`xxdg-open`
    * 如果没有，创建一个就行
    * 这个键也有可能叫`Browser`，有的话将两个键的值都设置成`xxdg-open`就行
    * **如果你有自定义PATH变量，请先确保新的PATH变量已经生效了**

5. 在游戏启动前运行`startbrowserfix`脚本即可启动脚本

6. 启动游戏，随便点开一个公告里的链接看看

7. 游戏结束后，运行`endbrowserfix`结束脚本

## 自定义
基本上所有东西都写注释里了，看脚本内容就行

## 原理
通过xxdg-open将调用的URL写到指定的文件里再让browserfix读取并执行，可以避免通过wine调用导致继承环境变量之类的东西让浏览器出错(例如针对某一游戏配置的LD_PRELOAD、LD_LIBRARY_PATH)

~~省流：既然直接调用会出毛病，那不直接调用不就行了（~~