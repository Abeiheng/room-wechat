---
title: "Wander[001] - 未来流浪者：微信中的科幻机器人 V2.1"
author: sunyuqian1997
categories: article
tags:
  - blog
  - study
  - introduction
image: /assets/2021/08-future-wander-bot-001/conv1.webp
---

 > 作者: [起司](https://github.com/sunyuqian1997)，[扣扣](https://github.com/chelys-cheng)

## 项目简介

![cover](/assets/2021/08-future-wander-bot-001/cover.webp)

Wander [ 001 ]是一个以AI chatbot为主体的跨媒体互联网艺术项目，包括可交互的微信端机器人、CG影像、以及实时更新的地图网站。

参与者可以通过微信向Wander发送现实中的地点，Wander会从随机的“未来时间点”前往当地，返回科幻游记与街景图。参与者可以用行动指令，让Wander探索未知的地点，甚至与遇到的角色互动交流。

每一次的旅行的时间点是不确定的，而旅行的结果会实时记录于地图网站上。在人类的参与中，未来的地图会被不断完善，形成一个由公众与AI共同构建的科幻未来。艺术家基于Wander传送的游记与图像进行进一步CG创作，通过人机配合延展对未来的构想。

本项目展出于2021 Wave Summit,2021保利春季拍卖NFT展区与2021北京时代美术馆-亚洲数字艺术展。

截至2021年8月，已有超过1000名参与者带领Wander旅行。我们希望Wander能让人们重新审视熟悉的环境，从我们最熟悉的通讯软件里给人带去惊喜。

[AI Studio地址](https://aistudio.baidu.com/aistudio/projectdetail/2274223?forkThirdPart=1)
[代码详见Github](https://github.com/sunyuqian1997/Wander001-V2.1)

![conv2](/assets/2021/08-future-wander-bot-001/conv2.webp)

![tutorial](/assets/2021/08-future-wander-bot-001/tutorial.webp)

![show](/assets/2021/08-future-wander-bot-001/show.webp)

## 互动方式

![qrbode](/assets/2021/08-future-wander-bot-001/qrbode.webp)

扫码或微信搜索：WanderingBot，添加好友后即可互动。

发送 **我想去：xxxx**（任意中国大陆内地点）即可驱动Wander前去旅行。

降落后两分钟内发送 **行动：xxxx**（如：进入面前的建筑物，向身边的机器人打招呼）即可让Wander继续探索这个地点。

每次旅行可以发起两次行动，指令间隔需要在两分钟内。

![conv1](/assets/2021/08-future-wander-bot-001/conv1.webp)

## 实现流程

- 识别指令

&emsp;&emsp;指令系统`system/Command.py`将识别指令，并根据指令完成相应行为

- 旅行指令-[我想去：北京大门东门]

&emsp;&emsp;获取地理信息，如 \[北京大学东门\]

- **定位系统`system/Position.py`获取目标地点GPS坐标**

&emsp;&emsp;=》调用百度地图api地图检索功能，根据地点搜索获取gps坐标

&emsp;&emsp;&emsp;[http://lbsyun.baidu.com/index.php?title=webapi/guide/webservice-placeapi](http://lbsyun.baidu.com/index.php?title=webapi/guide/webservice-placeapi)

- **图像系统`system/RobotImage.py`获取过去景象**

&emsp;&emsp;=》调用百度地图api全景静态图功能，获取该坐标对应的街景图

&emsp;&emsp;&emsp;[http://lbsyun.baidu.com/index.php?title=viewstatic](http://lbsyun.baidu.com/index.php?title=viewstatic)

- **图像系统`system/RobotImage.py`拍摄未来照片**

&emsp;&emsp;=》调用PaddleHub风格迁移模型，迁移成未来风格

&emsp;&emsp;&emsp;[https://aistudio.baidu.com/aistudio/projectdetail/439779?channelType=0&channel=0](https://aistudio.baidu.com/aistudio/projectdetail/439779?channelType=0&channel=0)

- **思维系统`system/Thinking.py`形成旅行日志**

&emsp;&emsp;=》调用彩云小梦api，生成游记

&emsp;&emsp;&emsp;[https://open.caiyunapp.com/%E5%BD%A9%E4%BA%91%E5%B0%8F%E6%A2%A6API](https://open.caiyunapp.com/%E5%BD%A9%E4%BA%91%E5%B0%8F%E6%A2%A6API)

- **存储系统`system/Storage.py`保存旅行日志**

- **通讯信息回复用户**

&emsp;&emsp;=》通过WeChaty返回消息给用户

&emsp;&emsp;&emsp;[https://wechaty.js.org/](https://wechaty.js.org/)

- 行动指令-[行动：扒开废墟碎片找到通道]

&emsp;&emsp;=》获取行动内容，如[扒开废墟碎片找到通道]，结合前文内容

- **思维系统`system/Thinking.py`形成行动日志**

&emsp;&emsp;=》调用彩云小梦api，生成游记

&emsp;&emsp;&emsp;[https://open.caiyunapp.com/%E5%BD%A9%E4%BA%91%E5%B0%8F%E6%A2%A6API](https://open.caiyunapp.com/%E5%BD%A9%E4%BA%91%E5%B0%8F%E6%A2%A6API)

- **存储系统`system/Storage.py`保存行动日志**

- **通讯信息回复用户**

&emsp;&emsp;=》通过WeChaty返回消息给用户

## 准备工作

- WeChaty Token申请地址：

&emsp;[http://pad-local.com](http://pad-local.com)

- 百度地图的api Token(ak)可通过在官网控制台创建应用获得，需付费

&emsp;[http://lbsyun.baidu.com/index.php?title=%E9%A6%96%E9%A1%B5](http://lbsyun.baidu.com/index.php?title=%E9%A6%96%E9%A1%B5)

- 彩云小梦的api Token需要通过邮件申请

&emsp;[https://open.caiyunapp.com/%E5%BD%A9%E4%BA%91%E5%B0%8F%E6%A2%A6API](https://open.caiyunapp.com/%E5%BD%A9%E4%BA%91%E5%B0%8F%E6%A2%A6API)

## 部署步骤

### 安装docker

- 可以在[官方教程](https://docs.docker.com/engine/install)上找到不同系统上安装docker的方法，如[Ubuntu安装Docker指南](https://docs.docker.com/engine/install/ubuntu/)
- 安装完毕后，可通过`docker version`查看是否安装成功

### 启动wechaty puppet服务网关容器

```python
docker run -d \
    --restart=always \
    --name wechaty_puppet_service_token_gateway \
    -e WECHATY_LOG=verbose \
        -e WECHATY_PUPPET=wechaty-puppet-padlocal \
        -e WECHATY_TOKEN=1c468a07-9d85-4af4-945a-db7238b53189 \
        -e WECHATY_PUPPET_PADLOCAL_TOKEN=puppet_padlocal_xxxxx \
        -e WECHATY_PUPPET_SERVER_PORT=8081 \
        -p "8081:8081" \
    wechaty/wechaty:latest
```

注：

- `WECHATY_TOKEN`表示自定义的一个唯一令牌，需要唯一，本文设置使用的是生成的UUID，可以参考，如果提示错误可替换，后续检测网关有效性有用到
- `WECHATY_PUPPET_PADLOCAL_TOKEN`即从wechaty获取的有效token，格式为`puppet_padlocal_xxxxx`，可自行替换成自己的token
- `WECHATY_PUPPET_SERVER_PORT`表示与官方服务器通信的端口，后续检测网关有效性有用到

部署正常的话，docker容器内部的log应该会出现以下内容：

```python
============================================================
 Welcome to Wechaty PadLocal puppet!
 - wechaty-puppet-padlocal version: 0.4.1
 - padlocal-ts-client version: 0.4.0
============================================================
```

而Wechaty官方给出检测有效性的方式为访问网址：

```url
https://api.chatie.io/v0/hosties/1c468a07-9d85-4af4-945a-db7238b53189
```

`https://api.chatie.io/v0/hosties/`后面的字符串即为上文提到的`WECHATY_TOKEN`的值。

当结果为以下内容：

```json
{"host":"xxx.xxx.xxx.xxx","ip":"xxx.xxx.xxx.xxx","port":8081}
```

`host`和`ip`分别为你网关部署服务器的Host和IP地址，`port`即为前文提到的`WECHATY_PUPPET_SERVER_PORT`参数对应的值。

如果`host`和`ip`为实际的值，而不是0.0.0.0，则表示网关部署成功啦。

### 启动mysql数据库容器

```python
docker run -d \
    --name wander_storage \
    -e MYSQL_ROOT_PASSWORD=123456 \
    -e MYSQL_DATABASE=wander_storage \
    -e MYSQL_USER=wander \
    -e MYSQL_PASSWORD=wander \
    -p "3306:3306" \
    mysql:5.7
```

### 启动redis数据库容器

```python
docker run -d \
    --restart=always \
    --name cache_redis \
        -p "6379:6379" \
    redis:latest
```

### pip安装运行环境所需模块

`pip install -r ./work/requestments.txt`

### 运行Wander

`python ./work/robot-start.py`

## 总结

本项目是[在未来流浪：基于WeChaty, PaddleHub与彩云小梦的科幻机器人](https://aistudio.baidu.com/aistudio/projectdetail/1896705)的升级版本。基于上个版本，进行了全面的代码重构并新增“行动”功能，新增后端网站记录，完善图片迁移。本项目仅包含微信机器人部分。

本项目由速冻乱码搅拌机开发。

设计/ [me](https://github.com/sunyuqian1997)  

Chatbot开发/ [扣扣](https://github.com/chelys-cheng) , [me](https://github.com/sunyuqian1997)

后端/[扣扣](https://github.com/chelys-cheng)

前端/[Shing](https://github.com/shing19)，[Ray](https://github.com/Ray-lei-blog)

协助/[草莓](https://github.com/Fairywang9)，[koi](https://github.com/YingXu-Koi)

文本续写AI/彩云科技

![logo](/assets/2021/08-future-wander-bot-001/logo.webp)
