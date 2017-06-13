# 切换频道

## 示例1 打开CCTV1高清

### DA输出
- domain:
    - tv.live
 - intent
     - "tv.live.channel.search"
 - slot
     - "channel_name"："CCTV1"
     - "resolution": "高清"
### Bot输出
```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "SwitchChannel",
            "message_id" : "message-2142"
        },
        "payload": {
            "channel_name": "CCTV1高清",
            "channel_code": "cctv1_hd",
            "extend": {}
        }
    }
```

## 示例2 我想看9频道
### DA输出
- domain:
    - tv.live
 - intent
     - "tv.live.channel.search"
 - slot
     - "channel_number"："9"
### Bot输出
```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "SwitchChannel",
            "message_id": "message-id-123123"
        },
        "payload": {
            "channel_num": "9",
            "extend": {}
        }
    }
```
## 示例3 我想看直播节目
### DA输出
- domain:
    - tv.live
 - intent
     - "tv.live.channel.search"
### Bot输出
```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "SwitchChannel"
        },
        "payload": {
            "extend": {}
        }
    }
```
# 播放节目
## 示例1 CCTV1高清的新闻联播
### DA输出
- domain:
    - tv.live
 - intent
     - "tv.live.program.search"
 - slot
     - "channel_name"："CCTV1"
     - "resolution": "高清"
     - "program_name": "新闻联播"
### Bot输出
```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "ReplayProgram",
            "message_id" : "message-id-123"
        },
        "payload": {
            "channel_name": "CCTV1高清",
            "channel_code": "cctv1_hd",
            "program_name": "新闻联播"，
            "extend": {}
        }
    }
```

## 示例2 回看CCTV1昨天的节目
### DA输出
- domain:
    - tv.live
 - intent
     - "tv.live.program.search"
 - slot
     - "channel_name"："CCTV1"
     - "play_time": "2017-05-18 0:0:0,2017.05.18 23:59:59"

### Bot输出
```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "ReplayProgram",
            "message_id":"message-id-1213213"
        },
        "payload": {
            "channel_name": "CCTV1",
            "channel_code": "cctv1",
            "time": "2017-05-18 0:0:0,2017.05.18 23:59:59"
            "extend": {}
        }
    }
```

## 示例3 我想看9频道昨天的节目
###DA输出
- domain:
    - tv.live
 - intent
     - "tv.live.program.search"
 - slot
     - "channel_number"："9"
     - "play_time": "2017-05-18 0:0:0,2017.05.18 23:59:59"

### Bot输出

```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "ReplayProgram",
            "message_id":"message-id-123123"
        },
        "payload": {
            "channel_number": "9",
            "time": "2017-05-18 0:0:0,2017.05.18 23:59:59"
            "extend": {}
        }
    }
```

## 示例4 回看节目
### DA输出
- domain:
    - tv.live
- intent
     - "tv.live.program.search"
### Bot输出
```
    {
        "header": {
            "namespace": "tv.command.live",
            "name": "ReplayProgram"
        },
        "payload": {
            "extend": {}
        }
    }
```
