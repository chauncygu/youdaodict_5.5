![Screencast](https://2.bp.blogspot.com/-a1ldr3X2U1s/WZAIrNamPxI/AAAAAAAAAjw/CGVeNEUzjWk2pK71C4PwuMIzRFwc9ROawCLcBGAs/s1600/youdao.png)
### 有道词典 v1.1.1 ( 支持 PyQt 5.5 或以上 )
这个有道词典是从 Deepin 15.4.1 (youdao-dict_1.0.8-1_amd64.deb) 取出, 然后重新打包成 Ubuntu 能用的 deb 安装包<br>
它支持 Ubuntu 16.10 / Fedora 24 / OpenSUSE 42.2 等开始的 Linux 分发版<br>
http://packages.deepin.com/deepin/pool/main/y/youdao-dict/

1) 取得有道词典安装包 (需要3D加速, 假设显卡驱动已安装了)
```
$ wget https://github.com/yomun/youdaodict_5.5/raw/master/youdao-dict_1.1.1-0~ubuntu_amd64.deb
```
2) 检查 pip3 上安装的 PyQt5 (pip3 命令的安装可看步骤3)<br>
https://pypi.org/project/PyQt5/
```
$ su

$ pip3 list | grep PyQt5
PyQt5       5.12.1
PyQt5-sip   4.19.15

$ pip3 show PyQt5
Name: PyQt5
Version: 5.12.1
Summary: Python bindings for the Qt cross platform UI and application toolkit
Home-page: https://www.riverbankcomputing.com/software/pyqt/
Author: Riverbank Computing Limited
Author-email: info@riverbankcomputing.com
License: GPL v3
Location: /usr/local/lib/python3.6/dist-packages
Requires: PyQt5-sip
Required-by:

如上信息可知道这个 PyQt5 不是来自本身 Linux 软件库 (/usr/lib/python3/dist-packages), 撤..

$ pip3 uninstall PyQt5 PyQt5-sip

也不要用非root户口安装上 PyQt5, 其路径应该是
/home/$USERNAME/.local/lib/python3.6/site-packages
有的话, 也要撤.. 同以上方法, 只是不用 su 转换成 root 权限
```
3) 安装依赖软件包
- Ubuntu 16.04 - 20.04 / Debian 9.1 / Linux Mint 18.2 / Zorin OS 12.1 (可以跳过)
```
$ su
$ apt install python3 python3-pip python3-xdg python3-xlib

$ apt install python3-dbus python3-lxml python3-pil python3-requests
$ apt install python3-pyqt5 python3-pyqt5.qtmultimedia python3-pyqt5.qtquick python3-pyqt5.qtwebkit

$ apt install gir1.2-appindicator3-0.1 qml-module-qtgraphicaleffects qml-module-qtquick-controls
$ apt install libqt5multimedia5-plugins ttf-wqy-microhei
$ apt install tesseract-ocr tesseract-ocr-eng tesseract-ocr-chi-sim tesseract-ocr-chi-tra

$ apt install ubuntu-restricted-extras

Ubuntu 18.04 用 fonts-wqy-microhei 取代了 ttf-wqy-microhei
```
- Fedora 26 - 29
```
$ touch ~/.Xauthority

$ su
$ dnf install python3 python3-pip python3-pyxdg python3-xlib

$ dnf install python3-dbus python3-lxml python3-pillow python3-requests
$ dnf install python3-qt5 python3-qt5-devel python3-qt5-webkit
$ dnf install libappindicator-gtk3 qt5-qtgraphicaleffects qt5-qtquickcontrols qt5-qtbase-devel
$ dnf install tesseract-devel tesseract-langpack-enm
$ dnf install tesseract-langpack-chi_sim tesseract-langpack-chi_tra

旧版的软件库没提供 python3-xlib 的话, 可以用 pip3 安装之..
$ pip3 install --upgrade pip
$ pip3 install python3-xlib
```
- OpenSUSE Tumbleweed
```
$ su
$ zypper install python3 python3-pip python3-pyxdg python3-python-xlib

$ zypper install python3-lxml python3-Pillow python3-requests python3-qt5 python3-qt5-devel
$ zypper install typelib-1_0-AppIndicator3-0_1 libqt5-qtgraphicaleffects libqt5-qtquickcontrols
$ zypper install python3-dbus-python libQt5WebKit5 libQt5WebKitWidgets5
$ zypper install tesseract-ocr-devel tesseract-ocr-traineddata-english
$ zypper install tesseract-ocr-traineddata-chinese_simplified
$ zypper install tesseract-ocr-traineddata-chinese_traditional

旧版的软件库没提供 python3-python-xlib 的话, 可以用 pip3 安装之..
$ pip3 install --upgrade pip
$ pip3 install python3-xlib
```
- Antergos 17.8 - 19.3 / Manjaro 17.0.4 - 18.0.4
```
$ su
$ pacman -S python python-pip python-xdg python-xlib
$ pacman -S python-dbus python-lxml python-pillow python-requests python-pyqt5 pyqt5-common
$ pacman -S qt5-graphicaleffects qt5-multimedia qt5-quickcontrols qt5-webkit qt5-base
$ pacman -S libappindicator-gtk3 wqy-microhei binutils
$ pacman -S tesseract tesseract-data-eng tesseract-data-chi_sim tesseract-data-chi_tra
```
- Manjaro 17.0.2
```
安装方法跟以上 Antergos 一样, 但运行 youdao-dict 可能会出现
Cannot mix incompatible Qt library (version 0x50701..
这样的错误, 解决方法是重安装 qt5-styleplugins (安装 aurget 以重安装)

$ pacman -Rsn qt5-styleplugins
$ pacman -Syyu

$ pacman -S wget base-devel

$ su $USERNAME

$ wget https://github.com/pbrisbin/aurget/archive/v4.7.2.tar.gz
$ tar -xvf v4.7.2.tar.gz && cd aurget-4.7.2 && sudo make install

$ aurget -S qt5-styleplugins
```
- Solus OS 3 - 4
```
$ su
$ pip3 install --upgrade pip
$ pip3 install pyxdg
$ pip3 install python3-xlib

$ eopkg install python3 python3-dbus python-lxml python-pillow python-requests python3-qt5
$ eopkg install libappindicator qt5-graphicaleffects qt5-multimedia qt5-quickcontrols qt5-webkit
$ eopkg install tesseract tessdata

$ eopkg install binutils
```
4) 安装有道词典
```
$ su

如果是 dpkg 安装的话 (基于 Ubuntu / Debian / Linux Mint / Zorin OS)
$ dpkg -i youdao-dict_1.1.1-0?ubuntu_amd64.deb
$ apt install -f  (如果上面的 dpkg 命令运行显示缺依赖软件包)

如果是 tar 安装的话 (其实就是将 deb 解压, 把文件放到系统各处)
$ ar vx youdao-dict_1.1.1-0?ubuntu_amd64.deb
$ tar -Jxvf data.tar.xz -C /
$ rm -rf control.tar.gz && rm -rf data.tar.xz && rm -rf debian-binary
```
5) 运行 youdao-dict (用非root户口)
```
如果点击有道词典图标, 但不能打开..

$ su $USERNAME
$ xhost + && youdao-dict

遇到 Xlib.error.DisplayConnectionError: Can't connect to display “:0”: b'No protocol specified\n' 问题
则需要 xhost + 指令, 这是 python-xlib 引起的 bugs
```
6) 卸载
```
$ rm -rf ~/.config/youdao-dict
$ rm -rf ~/.cache/youdao-dict

$ su

如果是 dpkg 安装的话
$ dpkg -r youdao-dict

如果是 tar 安装的话
$ wget https://raw.githubusercontent.com/yomun/youdaodict_5.5/master/youdaodict-uninstall.sh
$ bash youdaodict-uninstall.sh
```
- 图标不能显示问题
```
$ su
$ rm -rf /usr/share/icons/hicolor/icon-theme.cache
```
- PYTHONPATH 环境变量
```
如果依赖软件包安装完后,
还是会出现 ModuleNotFoundError: No module named 'PyQt5.QtWebKitWidgets'
先检查是否用 pip3 安装了 PyQt5, 如有就卸载

如还不行, 建议加入 PYTHONPATH 环境变量

$ python3
Python 3.6.7 (default, Oct 22 2018, 11:32:17) 
[GCC 8.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> print(os.sys.path)
['', '/usr/lib/python36.zip', '/usr/lib/python3.6', '/usr/lib/python3.6/lib-dynload',
 '/usr/lib/python3/dist-packages']

选一个以上可用的路径为 $PYTHONPATH

$ su root
$ gedit /usr/share/applications/youdao-dict.desktop

### Exec=youdao-dict %f
Exec=env PYTHONPATH=/usr/lib/python3/dist-packages youdao-dict %f

也可以在 ~/.bashrc 或 ~/.profile 加入

$ su $USERNAME
$ gedit ~/.bashrc 或 gedit ~/.profile

export PYTHONPATH=$PYTHONPATH:/usr/lib/python3/dist-packages

然后运行

$ source ~/.bashrc 或 source ~/.profile
$ youdao-dict
```
