[toc]


# Step By Step
1. 编写自定义指令文件:intent.dic,dict.dic,command.dic。必须是gbk编码格式
2. 首先编写意图文件intent.dic,意图文件包含了自定义指令的意图集合。每个意图包含domain、intent、指令模板信息，格式为‘domain’+空格+‘intent’+空格+‘指令模板信息’，每一行不超过128字节。
示例如下:
* 注 第一列固定命名：ai.dueros.device_interface.thirdparty.厂商名.指令名，厂商名和指令名自行拟定；第二列采用驼峰命名法；
```
#gb18030
ai.dueros.device_interface.thirdparty.XXXTV.tv_command Open 打开[device]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command Close 关闭[model][W:0-2]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command Upgrade 升级
ai.dueros.device_interface.thirdparty.XXXTV.tv_command Upgrade [D:check]系统更新
ai.dueros.device_interface.thirdparty.XXXTV.tv_command SwitchMode [model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command AutoSet 调正画面
ai.dueros.device_interface.thirdparty.XXXTV.tv_command SwitchChannel 调到[F:Num->slot_name]频道
ai.dueros.device_interface.thirdparty.XXXTV.tv_command Cooking [F:time]提醒我起床
```
## 模板信息，支持以下4类模板信息。
>[slot_name]表示槽位信息。在与用户的指令进行匹配时，对匹配的内容进行提取，保存在名为slot_name的槽位中，并返回给设备端。slot_name必须在dict.dic中有相应的词典定义。
>[D:slot_name]表示一个匹配词，在与用户的指令进行匹配时，匹配到的内容不会进行提取，也不会返回给设备端。slot_name必须在dict.dic中有相应的词典定义。
>[W:0-2]表示可以匹配0到2个字节长度的任意字符，系统限定最长通配为4个字节。W:0-2不需要在dict.dic中进行定义
>[F:Num]表示可以匹配任意的连续数字的系统函数。不需要在dict.dic中进行定义，默认返回的槽位名为：num。可用F:Num->slot_name进行槽位名的改写，则此时返回的槽位名为：slot_name
>[F:time]表示可以对时间进行匹配的系统函数。不需要在dict.dic中进行定义，默认返回的槽位名为：time。可以解析三种时间类型：50秒，今天早上，5点到8点。

3.编写词表文件dict.dic,其中包括词表[D:device], [D:model], [D:check]
词表表头均需以[D:xxx]开始命名。
dict.dic文件如下
```
#gb18030
[D:device]
光盘
光机
电视
投影
设置页面
设置
网络连接
[D:model]
3D模式
正装正投
正装背投
吊装正投
吊装背投
正装吊头
[D:check]
检查
```

4、编写command.dic文件，command.dic中包含了所有的QueryList,既所有的自定义指令。
command.dic示例：
```
打开光盘
打开光机
打开电视
关闭吊装背投
关闭吊装背投吧
调到3频道
9点提醒我起床
```

按照以上步骤就完成了自定义指令文件的编写，需要将此三个文件上传至dueros开发者平台。

进入开发者设备控制台：https://dueros.baidu.com/didp/product/listview，进入相应的设备
点击左侧的“云服务配置”
下拉后即可看到自定义控制指令上传文件的界面。

上传成功，并收到百度邮件后即可使用自定义指令，自定义指令的返回结果示例如下：

> "正装正投"
```
{
    "header": {
        "namespace": "ai.dueros.device_interface.thirdparty.XXXTV.tv_command",
        "name": "SwitchModel"
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
        "namespace": "ai.dueros.device_interface.thirdparty.XXXTV.tv_command",
        "name": "Open"
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
        "namespace": "ai.dueros.device_interface.thirdparty.XXXTV.tv_command",
        "name": "Close"
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
        "namespace": "ai.dueros.device_interface.thirdparty.XXXTV.tv_command",
        "name": "AutoSet"
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
        "namespace": "ai.dueros.device_interface.thirdparty.XXXTV.tv_command",
        "name": "SwitchChannel"
    },
    "payload": {
        "slot_name": 5
    }
}
```
---

> "检查系统更新" 和 "升级"
```
{
    "header": {
        "namespace": "ai.dueros.device_interface.thirdparty.XXXTV.tv_command",
        "name": "Upgrade"
    },
    "payload": {
    }
}
```

