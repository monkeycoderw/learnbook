简述
Ubuntu16.04安装完后，和12.04以及14.04都不一样，并没有中文输入功能。于是搜索一些安装中文输入法的方法。 
开始安装了ibus pinyin输入法，但是系统重启之后发现有些时候不稳定，无法切入到中文输入。最后还是换用搜狗输入法了，用下来目前都很好用。

ibus输入法
Chinese语言包安装
首先需要给Ubuntu16.04安装Chinese语言包支持。 
这里写图片描述 
如上图点击其中的Install/Remove Languages…，这个对话框是通过system settings–>Language Support选择弹出来的。 
然后再在Install/Remove Languages…弹出的对话框中将Chinese语言包安装上： 
这里写图片描述

ibus输入法安装
在中文语言包安装完成后，就需要安装ibus输入法了，需要在Terminal中输入：

sudo apt-get install ibus ibus-clutter ibus-gtk ibus-gtk3 ibus-qt4
1
来安装ibus框架。用

im-config -s ibus
1
切换到ibus框架。再安装拼音引擎：

sudo apt-get install ibus-pinyin
1
再调出ibus Preference来添加该拼音输入法：

sudo ibus-setup
1
在弹出对话框中 
这里写图片描述 
添加Chinese-Pinyin输入法。这样, ibus 拼音输入法就安装配置好了。

系统输入法设置
在System Settings–>Text Entry中添加上ibus拼音输入法，并将Show current input source in the menu bar勾选上，这样就会在系统的菜单条上显示输入法切换的图标了。

Fcitx输入法
Fcitx输入法安装与配置与ibus相似，这两者都比较好用的，可以搜索详细步骤。

搜狗输入法安装
参考了搜狗输入法安装这篇文章，步骤一致，效果可行。