怎么说呢，我印象中针对华为Atlas 200dk的开发是比较痛苦，连续几次干红温了😡。首先遇到的一个困难就是华为官方教程中涉及的部分网页已经打不开了。其次是制板结束后过了一个晚上发现整个OS莫名消失了。😖不幸中的万幸是当时写了这么一个开发过程记录。

# 华为Atlas 200 dk开发过程记录
## 一键制卡
现在一键制卡非常方便（主要是你也找不到对应的UBuntu版本和CANN版本了）。网上教程很多的，而且都非常详细。在这里就不多说了。
## 环境搭建
### 采用开发环境和运行环境（合设）法
采用开发环境和运行环境**合设的方式其实在一键制卡的过程中已经把开发环境和运行环境全部搭建好了**，只需要配置并连接一下Atlas200dk的网络 | 安装一下Python3.7.5和安装VS Code并进行ssh连接就行。
#### 配置网络
具体可以参照B站视频：![Atlas200dk网络配置](https://www.bilibili.com/video/BV1LA4y1Q7cW?p=4)中的介绍。如果想快速一点的话就是这样子：<br>
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
vi /etc/systemd/resolved.conf #修改DNS为114.114.114.114
```
```
systemctl restart systemd-resolved.service
```
### Python3.7.5的安装
在终端中输入（注意大小写）：
```
wget https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz
```
随后输入指令：
```
sudo apt-get install -y gcc g++ make cmake zlib1g zlib1g-dev libbz2-dev libsqlite3-dev libssl-dev libxslt1-dev libffi-dev unzip pciutils net-tools libncursesw5-dev
```
随后解压缩Python3.7.5的安装包
```
tar zxvf Python-3.7.5.tgz
```
紧接着进入Python-3.7.5目录内
```
cd Python-3.7.5
```
输入命令：
```
./configure --prefix=/usr/local/python3.7.5 --enable-loadable-sqlite-extensions --enable-shared
```
随后，输入命令充分调用CPU编译：
```
make -j8
```
接下来，输入指令：
```
sudo make install
```
到这里，PYthon的安装还没有结束（但是快了，剩下就是配一个环境）。<br>
随后在终端中输入以下命令，安装相应的Python文件：
```
sudo ln -s /usr/local/python3.7.5/bin/python3 /usr/local/python3.7.5/bin/python3.7.5
sudo ln -s /usr/local/python3.7.5/bin/pip3 /usr/local/python3.7.5/bin/pip3.7.5
```
完整后，再在终端中输入命令：
```
vi ~/.bashrc
```
随后滑动到最下面，将以下文本复制粘贴
```
#用于设置python3.7.5库文件路径
export LD_LIBRARY_PATH=/usr/local/python3.7.5/lib:$LD_LIBRARY_PATH
#如果用户环境存在多个python3版本,则指定使用python3.7.5版本
export PATH=/usr/local/python3.7.5/bin:$PATH
```
完成后，按`Esc + ： + w + q`键退出程序，随后输入命令：
```
source ~/.bashrc
```
完成后，查看当前环境中的Python版本：
```
python3.7.5 --version
```
应该能看到以下结果：<br>
![Python版本查看](https://github.com/StrayerSQH/stochastic-search/blob/main/%E5%85%B6%E4%BB%96%E6%94%AF%E6%8C%81%E6%9D%90%E6%96%99/%E5%8D%8E%E4%B8%BAAtlas%20200%20dk/Python%E7%89%88%E6%9C%AC%E6%9F%A5%E7%9C%8B.jpg)
随后运行`pip`指令查看：
```
pip3.7.5 --version
```
应该能看到以下结果：
![pip查看python版本](https://github.com/StrayerSQH/stochastic-search/blob/main/%E5%85%B6%E4%BB%96%E6%94%AF%E6%8C%81%E6%9D%90%E6%96%99/%E5%8D%8E%E4%B8%BAAtlas%20200%20dk/Pip%E6%9F%A5%E7%9C%8BPython%E7%89%88%E6%9C%AC.jpg)
到这里，Python包就安装好啦！！！<br>
如果还向安装一些其他的库的话，可以参照![其可能遇到的困难](https://github.com/StrayerSQH/Learning/blob/main/%E7%A1%AC%E4%BB%B6%E5%BC%80%E5%8F%91/%E5%8D%8E%E4%B8%BAAtlas200dk/%E5%85%B6%E4%BB%96%E5%8F%AF%E8%83%BD%E9%81%87%E5%88%B0%E7%9A%84%E5%9B%B0%E9%9A%BE.md)中的**3.Linux中的pip3指令安装Python库（同样适用于Atlas）**和**4.Atlas中关于python2 | pip | python3.6 | python3.7和pip3之间的关系以及环境配装**中的方式进行解决。

#### VS Code安装及ssh连接
VS Code可以直接从Ubuntu的商店中下载，非常方便。下载好后打开VS Code,在扩展处搜索`remote-ssh`扩展包点击安装就行。随后在最左下角的一个类似于这样的符号`><`的地方点一下，将Atals主机的名字：`HwHiAiUser@192.168.1.2`输入进去，随后输入密码：`Mind@123`并回车就行。
