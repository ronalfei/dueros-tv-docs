# 用户功能引导

## 摘要

本接口提供了用户功能引导所需要的指令和事件


## PlayGuideVideo指令

设备端收到该指令，应该调起视频播放器，并播放视频。

### 消息样例

```json

"directive": {
  "header": {
    "namespace": "ai.dueros.device_interface.extensions.user_guide",
    "name": "PlayGuideVideo",
    "messageId": "message_id-1244",
    "dialogRequestId": "dialog_request_id-1244"
  },
  "payload": {
    "token": "token-1244",
      "videoUrl": "http://www.baidu.com/tcl/guide_video.mp4"
```
### Payload参数说明

- token
 - 该结果的唯一标记
- videoUrl
 - 视频的url地址

## RenderGuidePage指令

设备端收到该指令，根据结果渲染引导页面。

### 消息样例

```json
"directive": {
  "header": {
    "namespace": "ai.dueros.device_interface.extensions.user_guide",
    "name": "RenderGuidePage",
    "messageId": "message_id-1244",
    "dialogRequestId": "dialog_request_id-1244"
  },
  "payload": {
    "token": "token-1244",
    "guideItems": [
      {
        "priority": 1,
        "title": "电视点播",
        "querys": ["我想看大鱼海棠", "经典电影", ...]
      },
      {
        "priority": 2,
        "title": "人脸识别",
        "querys": ["这个人是谁", "左边第一个女的是谁", ...]
      },
      ...
    ]
  }
}
```

###Payload参数说明

- token
 - 该结果的唯一标记
- guideItems
 - 引导条目列表
- guideItems[].priority
 - 该引导项目的优先级
- guideItems[].title
 - 该引导项目标题，如：”视频搜索“，”播放控制“
- guideItems[].querys
 - 该引导项目的语音query样例，如：”我要看变形金刚“，”播放第五个“
    
    
## RenderHint指令

渲染引导词。引导词是给用户的提示，提示用户当前可以输入哪些query

### 消息样例
```json
"directive": {
  "header": {
    "namespace": "ai.dueros.device_interface.screen",
    "name": "RenderHint",
    "messageId": "message_id-1244,
    "dialogRequestId": "dialog_request_id-1244"
  },
  "payload": {
    "token": "token-1244",
    "cueWords": [
      "播放长发公主",
      "回到主页",
      ...
    ]
  }
}
```
### Payload参数说明

- cueWords
 - 列表，可以有多个引导词
    

## 切换页面事件

当页面从A页面切换到B页面时，需要上报的事件，该事件通过LinkClicked进行上报
参见[screen.md](../screen-private.md)中的LinkClicked

LinkClicked中的payload为: 

```json
"payload": {
    "url":"dueros://user_guide.bot.dueros.ai/pageChanged?page_name=首页"
}
```

  - page_name
    - 切换到的页面名称



## 连续N次无结果的事件

当客户端连续n次收到无结果(no_result)之后上报该事件，该事件通过LinkClicked进行上报
参见[screen.md](../screen-private.md)中的LinkClicked

LinkClicked中的payload为: 

```json
"payload": {
    "url":"dueros://user_guide.bot.dueros.ai/noResult?count=4"
}
```

  - count
    - 连续无结果次数


## 时间段内无语音输入

客户端连续N秒没有语音输入后，需要上报的事件，该事件通过LinkClicked进行上报
参见[screen.md](../screen-private.md)中的LinkClicked

LinkClicked中的payload为: 

```json
"payload": {
    "url":"dueros://user_guide.bot.dueros.ai/timeout?seconds=10"
}
```

  - seconds
    - 超时的时常
