---
title: 使用shadowsocks科学上网
layout: post
date: 2015-03-23 12:00:00+0800
categories: 科学上网
author: xavier
---

因为工作中离不开Google，需要科学上网，从Squidy、 GAE 开始，到传说中稳定可靠的ssledge，一直到最近发现的Shadowsocks。

用了这么多，最方便也最放心的还是Shadowsocks。

#### 服务器选择

担心数据安全，也担心共享IP的服务不稳定，所以自己的独立IP是必须得有的。

测试速度、对比价格之后，选定 [搬瓦工](https://bandwagonhost.com/aff.php?aff=2511) 作为VPS，每年仅需4美元，且720P毫无压力。

注册之后，点击Services->Order New Services，然后选择Micro-64版本即可。

#### Ubuntu下的安装和配置

    apt-get install python-pip swig python-m2crypto
    
    pip install shadowsocks

配置文件(多端口多用户):

    {
        "server":"your_server_ip",
        "local_address": "127.0.0.1",
        "local_port":1080,
        "port_password":{
             "8989":"password0",
             "9001":"password1",
             "9002":"password2",
             "9003":"password3",
             "9004":"password4"
        },
        "timeout":600,
        "method":"aes-256-cfb",
        "fast_open": false
    }

配置文件（单用户）：

    {
        "server":"your_server_ip",
        "local_address": "127.0.0.1",
        "local_port":1080,
        "timeout":600,
        "password": "password",
        "method":"aes-256-cfb",
        "fast_open": false
    }

本文中，配置文件保存在 /etc/shadowsocks.json

#### 启动

后台启动

    nohup ssserver -c /etc/shadowsocks.json > /root/log &

并将该命令添加至/etc/rc.local。

#### 检查与自启动

新建check.sh。

    !/bin/bash
    if
    ps -ef|grep "shadowsocks on"|grep -v "grep"
    then
    echo "Status: Running"
    else
    echo "Status: Stopped"
    nohup ssserver -c /etc/shadowsocks.json > /root/log &
    fi

在命令行中执行：

    chmod +x /root/check.sh

设置自动执行该文件：

    crontab -e
    /5 * /root/check.sh

VPS推荐：[搬瓦工](https://bandwagonhost.com/aff.php?aff=2511)
