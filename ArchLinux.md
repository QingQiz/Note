## Arch Linux 的一些配置问题

### 电源管理

- 文件路径： `/etc/systemd/logind.conf`

### 输入法问题

- qt界面无法输入中文 (ibus)
    - `qtconfig-qt4`
        Interface -> Default Input Method -> iBus

    - 在 ~/.xprofile 添加
        ```shell
        export GTK_IM_MODULE=ibus
        export XMODIFIERS=@im=ibus
        export QT_IM_MODULE=ibus
        ```

    - 修改i3config 添加(修改) `exec --no-startup-id ibus-daemon --xim -d`

### 声音问题

- `pacman -S alsamixer pulsmixer`

- 声卡配置 `vim $HOME/.asoundrc`
    ```shell
    defaults.ctl.card 1
    defaults.pcm.card 1
    defaults.timer.card 1
    ```

### VIM

- YouComplete
    - `ln -s /usr/lib/libtinfo.so.6 /usr/lib/libtinfo.so.5`

### 包管理

- AUR: `vi /etc/pacman.d`

    ```conf
    [archlinuxcn]
    SigLevel = Optional TrustAll
    Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
    ```



### 触控板

- `pacman -S xf86-input-synaptics`

- 自然滚动
    `synclient VertScrollDelta=-66`

- 环形滚动
    `synclient CircularScrolling=1`

- 指针速度
    ```shell
    synclient MaxSpeed=xxx
    synclient MinSpeed=xxx
    ```

- 单击, 双击, 中键
    ```shell
    synclient TapButton1=1
    synclient TapButton2=3
    synclient TapButton3=2
    ```

### 网络问题

- wifi-menu "No network found"

    - `ip link set wlo1 up`

    - 如果出现
        > RTNETLINK answers: Operation not possible due to RF-kill

    - 则执行

        `rfkill unblock wifi`


### 蓝牙

- install `bliez` and `bluez-utils`, load `btusb` and start `bluetooth.service`
    ```shell
    pacman -S bluez
    pacman -S bluez-utils
    modprobe btusb
    systemctl start bluetooth.service
    ```


### Mathematica

- 打开mathematica时出错

    > `/opt/Mathematica/SystemFiles/FrontEnd/Binaries/Linux-x86-64/Mathematica: symbol lookup error: /usr/lib/libfontconfig.so.1: undefined symbol: FT_Done_MM_Var`
    - 解决方案
        Solution: [Mathematica and freetype-2.9 undefined symbol](https://forums.gentoo.org/viewtopic-p-8198000.html?sid=ab27c1ca8e1927691858595185e18284)

- mathematica 自动在`$HOME`创建`Wolfram Mathematica`
    - `pacman -S xdg-user-dirs`
    - `xdg-user-dirs-update`


### 其它的

- `pacman -Syu` 时显示

    > Possibly missing firmware for module: aic94xx
    > Possibly missing firmware for module: wd719x

- 解决方案

    https://gist.github.com/imrvelj/c65cd5ca7f5505a65e59204f5a3f7a6d

