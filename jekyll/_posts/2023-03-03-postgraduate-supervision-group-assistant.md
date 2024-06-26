---
title: "考研监督群管 - 考研路上的好帮手"
author: imooooc
categories:
  - article
image: /assets/2023/03-postgraduate-supervision-group-assistant/cover_title.webp
tags:
  - chatbot
  - assistant
---

## 背景

打算考研了，自发组建了一个考研小组，目前主要是解决管理群聊的功能，每个成员都被要求在群里每日学习打卡，而群管需要进行记录，包括打卡，学习时长计算，缺卡提醒，定时消息通知，以及自动修改每日考研倒计时的标题等等。因此便想到了用wechaty做一个bot机器人管理员。

## 传统的监督方式

早些时候，我看有些群主或管理员每天都要手动对成员打卡情况进行统计，想下面这样

![image-0](/assets/2023/03-postgraduate-supervision-group-assistant/image-0.webp)

费时又费力，还有每天手动更改考研倒计时的，不仅不够及时准确，而且每天这么设置很是麻烦。![image-1](/assets/2023/03-postgraduate-supervision-group-assistant/image-1.webp)

向上述所说的那些事情，其实都是一些重复性的劳动，完全可以交给机器人来完成，因此我想到了使用**wechaty**来实现一个考研监督群管的功能。

## 目前实现的功能：

- [x]  定时消息通知
- [x]  定时自动修改群名
- [x]  记录群员打卡
- [ ]  ~~缺卡提醒~~
- [x]  学习时长计算
- [ ] ~~新人欢迎提醒~~
- [ ]  ~~群员退群提醒~~

## 打卡格式

提供两种简易和标准两种场景：

| 场景 | 功能描述                             | 说明                                           | 备注                                       |
| :--- | :----------------------------------- | ---------------------------------------------- | ------------------------------------------ |
| 简易 | @bot助理 打卡                        | 只打卡记录天数，不计算学习时长，表示今日已学习 | @bot助理 打卡                              |
| 标准 | @bot助理 打卡 + 空格 + 时间(单位：h) | 打卡，并记录学习时长                           | 时间单位为h，数字精确到1位小数（四舍五入） |

示例1：
@bot助理 打卡

示例2：
@bot助理 打卡 2.5h

## 实现的效果：

- 简易版模式

![image-2](/assets/2023/03-postgraduate-supervision-group-assistant/image-2.webp)

- 标准版模式

![image-3](/assets/2023/03-postgraduate-supervision-group-assistant/image-3.webp)

- 定时提醒以及更新群名“考研倒计时”

![image-4](/assets/2023/03-postgraduate-supervision-group-assistant/image-4.webp)

后续可能会对数据存储进行完善，目前数据量比较小，我是把所有学生的打卡数据记录在一个json文件里，以后可以考虑使用数据库并将操作封装成接口调用的形式。

同时可能会上新一些新的功能，比如当天晚上把学习过的内容发表一个总结出来，第二天由bot在早上进行提醒，以便对前一天所学知识进行巩固，还有缺卡提醒，如果学生连续3天没有进行打卡了，则由bot进行相应的提醒和激励等等。

这个机器人大大方便了我们的日常学习和生活，能让我们节省很多时间，相比其他考研监督群的管理来讲，不用每天手动修改考研倒计时，不用每天用个excel表格记录成员学习打卡情况，能够让我更加专注于考研本身，其他杂七杂八的事情交给机器人处理。最后，2024考研加油吧，今年必上岸，冲冲冲！
