# 华为Atlas 200dk遇到的困难及解决思路
## 1.Linux密码
在Linux中，用户在没有通过命令修改密码前，不论是普通用户（User)和超级用户（root），初始密码都默认为：123456.<br>
## 2.Linux无法打开终端（Terminal)
如果遇到Ubuntu无法打开终端的情况，首先尝试使用快捷键：
```
Ctrl+Alt+F5
```
如果不行，选择并打开操作系统中的设置按钮，选择语言为中文，重新启动下系统即可：<br>
![Linux无法打开终端（Terminal)](https://github.com/StrayerSQH/stochastic-search/blob/main/%E5%85%B6%E4%BB%96%E6%94%AF%E6%8C%81%E6%9D%90%E6%96%99/%E5%85%B6%E4%BB%96%E5%8F%AF%E8%83%BD%E9%81%87%E5%88%B0%E7%9A%84%E5%9B%B0%E9%9A%BE/Linux%E6%97%A0%E6%B3%95%E6%89%93%E5%BC%80%E7%BB%88%E7%AB%AF.jpg)<br>
这样问题就能够解决了。
## 3.Linux安装中文汉化及输入法(针对低版本情况）
打开终端，输入以下命令安装 IBus 和它的一些附加组件：
```
sudo apt-get update
sudo apt-get install ibus ibus-clutter ibus-gtk ibus-gtk3 ibus-qt4
```
比较流行的中文输入法引擎有 fcitx 和 ibus-pinyin（智能拼音），ibus-libpinyin（拼音），ibus-sunpinyin（孙拼音），和 ibus-rime（中州韵）等。<br>

以安装 ibus-libpinyin 为例，可以使用以下命令：
```
sudo apt-get install ibus-libpinyin
```
登出并重新登录您的系统。<br>
打开系统设置 > 地区和语言。<br>
如果没有添加中文区域设置，点击“管理已安装的语言”，添加简体中文或繁体中文语言支持，并应用更改。<br>
在“输入来源”部分，点击“+”号添加新的输入方法。<br>
在搜索框中输入 “Chinese” 或 “Pinyin” 来查找中文输入法。<br>
你可以通过点击屏幕右上角的输入法图标来选择不同的输入法，或者使用快捷键（通常默认是 Super+Space 或 Ctrl+Space）在不同的输入法之间切换。<br>
![中文版Ubuntu](https://github.com/StrayerSQH/stochastic-search/blob/main/%E5%85%B6%E4%BB%96%E6%94%AF%E6%8C%81%E6%9D%90%E6%96%99/%E5%85%B6%E4%BB%96%E5%8F%AF%E8%83%BD%E9%81%87%E5%88%B0%E7%9A%84%E5%9B%B0%E9%9A%BE/%E4%B8%AD%E6%96%87%E7%89%88Ubuntu.jpg)
至于安装百度输入法或者搜狗输入法，直接在火狐浏览器搜索就可以了。随后，回到语言支持的窗口，键盘输入法系统选择“fcitx”。关闭。重启Ubuntu。中英文切换就是shift键！！！<br>
![选择百度或搜狗输入法](https://github.com/StrayerSQH/stochastic-search/blob/main/%E5%85%B6%E4%BB%96%E6%94%AF%E6%8C%81%E6%9D%90%E6%96%99/%E5%85%B6%E4%BB%96%E5%8F%AF%E8%83%BD%E9%81%87%E5%88%B0%E7%9A%84%E5%9B%B0%E9%9A%BE/%E9%80%89%E6%8B%A9%E7%99%BE%E5%BA%A6%E6%88%96%E6%90%9C%E7%8B%97%E8%BE%93%E5%85%A5%E6%B3%95.png)

## 3.Linux中的pip3指令安装Python库（同样适用于Atlas）
因为Python2已经终结使命，所以以后只能在Python3的情况下安装库。而为了防止Python2强占进程，需要按照以下进行配置：
在root中输入：
```
which python3
```
得到返回的一个地址，随后输入：
```
vi ~/.bash_profile
```
将`which python3`得到的地址插入到：
```
PATH="/usr/bin:${PATH}"
export PATH
alias python="/usr/local/python3.7.5/bin/pip3"
```
这样以后在每次使用pip3命令前需要输入`source ~/.bash_profile`后再`pip3 install ......`安装相应的库：
```
source ~/.bash_profile
pip3 install opencv-contrib-python
```

## 4 Atlas中关于python2 | pip | python3.6 | python3.7和pip3之间的关系以及环境配装
首先需要注意的是，Atlas中似乎默认安装了python2 | pip | python3.6和低版本的pip3。如果直接在终端输入名使用pip命令将会造成一种打架的局面。因此，首先使用以下命令查看python2 | pip | python3.6和低版本的pip3究竟都在哪些文件夹下面：
```
whicn python
which pip
which python3.6
which pip3
```
找到这些的位置后，进入root用户输入命令将这些文件全部删除：
```
sudo rm -rf /etc/sur/python（地址）
```
随后，在按照![开发过程记录](https://github.com/StrayerSQH/stochastic-search/blob/main/%E5%AD%A6%E4%B9%A0%E8%B5%84%E6%96%99/%E5%8D%8E%E4%B8%BAAtals%20200%20dk/%E5%BC%80%E5%8F%91%E8%BF%87%E7%A8%8B%E8%AE%B0%E5%BD%95.md)开发过程记录里的安装Python3.7.5的方式把Python安装上。<br>
对于现在安装上的版本，其内置的pip3只是一个19.2的版本，已经被淘汰了无法继续使用，因此还需要输入以下命令将pip3升级到最新的24版本：
```
pip3 install --upgrade pip
```
更新到24版本后，以后安装库的时候就是直接使用`pip3 install (库名)`安装就可以了。**但是一定要注意: 在安装库的时候一定一定要切换到非root用户，不然关机后这些库就都没有了！！！**

## 5 Atlas200dk中的时间问题
Atals 200 dk中由于安装的Ubuntu18.04.4，每一次断电重新启动后都会将其自身内部的系统时间设置为2018年。所以在以后要使用`pip3`命令或者是`wget`命令前一定要县进入root用户。。先查看以下当前时间。如果时间不对，也需要修改以下，具体命令为：
```
date #查看时间
sudo date MMDDHHMMYYY.SS
```

## 6 为什么Atlas200dk连不上网络
这是因为采用的临时连接的方式。所以每一次Atlas重新连接后都要重新配置网络环境。具体的步骤为：<br>
In PC:
```
ifconfig -a #查看PC机和Atlas网卡名称
```
```
vi /etc/netplan/01-netcfg.yaml
```
```
network:
     version: 2
     renderer: NetworkManager
     ethernets:
            enx8ae1eb8499e5: #需要修改网卡名
                dhcp4: no
                addresses: [192.168.1.223/8]
                gateway4: 255.255.255.0
                nameservers:
                      addresses: [114.114.114.114]

```
```
netplan apply
```

```
echo "1" > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o enp0s3 -s 192.168.1.0/24 -j MASQUERADE #需要修改网卡名
iptables -A FORWARD -i enx26ff406c8d9b -o enp0s3 -m state --state RELATED,ESTABLISHED -j ACCEPT #需要修改网卡名
iptables -A FORWARD -i enx26ff406c8d9b -o enp0s3 -j ACCEPT #需要修改网卡名
```

In Atlas:
```
route add default gw 192.168.1.223 dev usb0
```
```
vi /etc/systemd/resolved.conf
```
```
systemctl restart systemd-resolved.service
```
