[toc]


# Step By Step
1. 找我们申请一个appid: dm95BBA8BD85310928
2.  利用appid建立一个文件夹, 在该文件夹里编写自定义文件
3. 首先编写意图文件intent.dic, 示例如下:
```
smart_tv \t open \t 打开[device]
smart_tv \t close \t 关闭[model]
smart_tv \t upgrade \t 升级
smart_tv \t upgrade \t [D:check]系统更新
smart_tv \t switch_mode \t [model]
smart_tv \t switch_mode \t [model]
smart_tv \t switch_mode  \t [model]
smart_tv \t switch_mode  \t [model]
smart_tv \t switch_mode  \t [model]
smart_tv \t autoset \t 调正画面
smart_tv \t switch_channel \t 调到[num]频道
```
> 第一列smart_tv不用变
> \t 是键盘上的tab键
> open就是对应的意图, 
> 最后一列就是用户输入的query
> [] 里的表示槽位, 也是会返回给用户的一个标识, 槽位也需要提供词表文件
> [D:xxx]里的xxx表示这是一个词表, 还需要在写一份xxx.dic的词表文件
> [num]是一个内置的词表, 无需提供, 他会专门匹配数字类型的值

4 .  填写词表文件device.dic, model.dic, check.dic
device.dic
```
光盘
光机
电视
投影
设置页面
设置
网络连接
``` 
model.dic
```
3D模式
正装正投
正装背投
吊装正投
吊装背投
正装吊头
```
check.dic
```
检查
```
按照以上步骤就完成了自定义指令的操作, 按照上面的例子, 我们列举几个返回结果:
> "正装正投"
```
{
    "header": {
        "namespace": "tv.personal",
        "name": "switch_model"
    },
    "payload": {
        "model": "正装正投"
    }
}
```
---
> "打开光机"
```
{
    "header": {
        "namespace": "tv.personal",
        "name": "open"
    },
    "payload": {
        "device": "光机"
    }
}
```
---

> "关闭3d模式"
```
{
    "header": {
        "namespace": "tv.personal",
        "name": "close"
    },
    "payload": {
        "device": "3D模式"
    }
}
```
---

> "调整画面"
```
{
    "header": {
        "namespace": "tv.personal",
        "name": "autoset"
    },
    "payload": {
    }
}
```
---

> "调到5频道"
```
{
    "header": {
        "namespace": "tv.personal",
        "name": "switch_channel"
    },
    "payload": {
        "channel": 5
    }
}
```
---

> "检查系统更新" 和 "升级"
```
{
    "header": {
        "namespace": "tv.personal",
        "name": "upgrade"
    },
    "payload": {
    }
}
```



# 其他描述
##  TV数据导入NLU平台目录结构

意图词表文件目录
------
     $NLUPATH/TV/{$appId}/intents/intent.dic

实体词表文件目录
------
     $NLUPATH/TV/{$appId}/entity/{$entity_name}.dic

意图词表文件格式
--------
     {vertical_name}\t{$intent_name}\t{pattern} 
      
实体词表
-----
     {word1}\r\n{word2}\r\n
     
pattern表达式
----------
    [slot_name][D:dic_name][W:1-9]
    
    [slot_name]表示槽位
    [D:dic_name]表示词典
    [W:1-9] 占位符，比如pattern为[W:1-8],则召回所有1-8个字节的query

样例
--
爱奇艺 

    appId=dm95BBA8BD85310928
> appid是分配给厂商的唯一id, 在自定义指令上是会通过appid来做区分的, 厂商没有的话, 可以找我们申请

实体词表文件存放的目录

    /home/work/nlu/TV/dm95BBA8BD85310928/intents/intent.dic

其中intent.dic的内容

    smart_tv \t 打开指令 \t 打开[device]
    smart_tv \t 打开指令 \t 打开[model]
    smart_tv \t 升级指令 \t 升级
    smart_tv \t 升级指令 \t [D:check]系统更新
    smart_tv \t 投影指令 \t 正装正投
    smart_tv \t 投影指令 \t 正装背投
    smart_tv \t 投影指令 \t 吊装正投
    smart_tv \t 投影指令 \t 吊装背投
    smart_tv \t 投影指令 \t 正装吊头
    smart_tv \t 调整指令 \t 调正画面
    smart_tv \ t调整指令 \t 调到频道[num]

自定义槽位词表device( `/home/work/nlu/TV/dm95BBA8BD85310928/entity/device.dic`)：

    光机
    电视
自定义词典check ( `/home/work/nlu/TV/dm95BBA8BD85310928/entity/check.dic`)：

    检测
    检查

num为系统内置词表不需要单独提供
