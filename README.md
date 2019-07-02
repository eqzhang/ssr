# SSR+SwitchyOmega翻墙

<a name="a62d8a1a"></a>
# 前提
需要准备一台海外服务器，这里是用的是搬瓦工vps

<a name="abe9cf92"></a>
# 创建一个目录存放SSR脚本

```bash
mkdir /ssr
wget https://github.com/eqzhang/ssr/blob/master/shadowsocksR.sh
```

<a name="2c4f83d1"></a>
# 执行shadowsocksR.sh脚本
![image.png](https://cdn.nlark.com/yuque/0/2019/png/211447/1554256157502-8d4b716b-f135-40ff-be2a-f17fd55a94f4.png#align=left&display=inline&height=887&name=image.png&originHeight=887&originWidth=680&size=76293&status=done&width=680)

![2019-04-03 10-06-40屏幕截图.png](https://cdn.nlark.com/yuque/0/2019/png/211447/1554257220015-05fd5a48-5116-4bac-8d02-50248ea8865e.png#align=left&display=inline&height=927&name=2019-04-03%2010-06-40%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE.png&originHeight=907&originWidth=665&size=63545&status=done&width=680)
<a name="2cc1f441"></a>
# 按回车继续，开始安装
<a name="811f543f"></a>
# 安装成功
![image.png](https://cdn.nlark.com/yuque/0/2019/png/211447/1554256898378-6ecf347f-8521-4237-948d-319a4e3b0a8f.png#align=left&display=inline&height=276&name=image.png&originHeight=276&originWidth=710&size=38120&status=done&width=710)
<a name="c1622a3e"></a>
# 启动，停止，重启ssr操作

```bash
/etc/init.d/shadowsocks start
/etc/init.d/shadowsocks stop
/etc/init.d/shadowsocks restart
```

<a name="172a0985"></a>
# 修改 ssr配置文件

```bash
vim /etc/shadowsocks.json
{
    "server":"0.0.0.0",
    "server_ipv6":"[::]",
    "server_port":10000,
    "local_address":"0.0.0.0",    //这里修改成0.0.0.0 全网段都可以访问
    "local_port":1080,
    "password":"eqzhang",
    "timeout":120,
    "method":"chacha20",
    "protocol":"auth_chain_a",
    "protocol_param":"",
    "obfs":"plain",
    "obfs_param":"",
    "redirect":"",
    "dns_ipv6":false,
    "fast_open":false,
    "workers":1
}
```

<a name="7599b675"></a>
# 启动ssr操作

```bash
[root@host ~]# cd /usr/local/shadowsocks/
[root@host shadowsocks]# python local.py -c/etc/shadowsocks.json   &
```

<a name="d1bef350"></a>
# 停止ssr操作

```bash
[root@host shadowsocks]# ps -ef |grep  py
root     24732     1  0 22:24 ?        00:00:00 python /usr/local/shadowsocks/server.py -c /etc/shadowsocks.json -d start
root     24746 13287  1 22:25 pts/0    00:00:00 python local.py -c /etc/shadowsocks.json
root     24756 13287  0 22:26 pts/0    00:00:00 grep --color=auto py
[root@host shadowsocks]# kill 24746
```

<a name="0e16902c"></a>
# 查看状态

```bash
[root@host shadowsocks]# netstat -lntp |grep py
tcp        0      0 127.0.0.1:1080          0.0.0.0:*               LISTEN      24746/python        
tcp6       0      0 :::10000                :::*                    LISTEN      24732/python
```

<a name="0284e82d"></a>
# SwitchyOmega插件下载
代理插件官网： [https://www.switchyomega.com/](https://www.switchyomega.com/)<br />离线插件文件：[https://github.com/eqzhang/ssr](https://github.com/eqzhang/ssr)

<a name="7f261a71"></a>
# Chrome安装插件
<a name="dac5b8da"></a>
## 方法一：

1. 打开Chrome浏览器，地址栏输入 `chrome://extensions/`
1. 将`.crx`的文件拖拽到浏览器中间，会出现`拖拽以安装的提示`，放入
1. 如果浏览器能直接安装即成功，如果不能安装，或者提示无法从该页面安装该程序，请参照方法三，如果提示安装包无效请参照方法二
<a name="89d5dfc8"></a>
## 方法二：

1. 将`.crx`的文件的扩展名改为`.zip`，并解压到指定的文件夹（这个文件夹不能删除, 例如解压到了test文件夹）
1. 打开Chrome浏览器，地址栏输入 `chrome://extensions/`, 勾择开发者模式，点击'加载已解压的扩展程序'
1. 选择你刚刚.zip`文件解压所在的test文件夹，点击确定。扩展程序列表出现你导入的扩展程序即为成功。
<a name="10233058"></a>
## 方法三：
在终端输入：<br />windows：（cmd）<br />`start chrome`<br />ubuntu：<br />`google-chrome --``enable``-easy-off-store-extension-``install`<br />mac：<br />`open -a "/Applications/Google Chrome.app`<br />打开谷歌浏览器后输入：<br />`chrome:``//extensions/`<br />将`.crx`的文件拖拽到浏览器中即可，如还有提示无法安装该程序则关闭chrome按上面步骤重新打开拖入

<a name="3c37007d"></a>
# SwitchyOmega设置
<a name="6664d365"></a>
# ![image.png](https://cdn.nlark.com/yuque/0/2019/png/211447/1554262344393-b84e8abe-dcf8-40c2-be1e-563c208295e2.png#align=left&display=inline&height=622&name=image.png&originHeight=622&originWidth=1040&size=71541&status=done&width=1040)

<a name="fa42bbb8"></a>
# 选择代理
![image.png](https://cdn.nlark.com/yuque/0/2019/png/211447/1554262068891-d2850de1-b5e6-487d-821c-5ec327436db5.png#align=left&display=inline&height=346&name=image.png&originHeight=305&originWidth=658&size=25987&status=done&width=746)

<a name="7606a3a6"></a>
# 翻墙成功
![image.png](https://cdn.nlark.com/yuque/0/2019/png/211447/1554262115705-2d689666-ed1c-4da7-9166-91ec2477f1b2.png#align=left&display=inline&height=848&name=image.png&originHeight=848&originWidth=1277&size=295833&status=done&width=1277)
