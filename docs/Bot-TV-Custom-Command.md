[toc]


# Step By Step
1. 找我们申请一个appid: dm95BBA8BD85310928
2.  利用appid建立一个文件夹, 在该文件夹里编写自定义文件
3. 首先编写意图文件intent.dic, 示例如下:
# 注 第一列固定命名：ai.dueros.device_interface.thirdparty.厂商名.指令名，第二列采用驼峰命名法
```
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t Open \t 打开[device]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t Close \t 关闭[model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t Upgrade \t 升级
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t Upgrade \t [D:check]系统更新
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t SwitchMode \t [model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t SwitchMode \t [model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t SwitchMode  \t [model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t SwitchMode  \t [model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t SwitchMode  \t [model]
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t AutoSet \t 调正画面
ai.dueros.device_interface.thirdparty.XXXTV.tv_command \t SwitchChannel \t 调到[num]频道
```
> 第一列ai.dueros.device_interface.thirdparty.XXXTV.tv_command不用变
> \t 是键盘上的tab键
> Open就是对应的意图, 
> 最后一列就是用户输入的query
> [] 里的表示槽位, 也是会返回给用户的一个标识, 槽位也需要提供词表文件
> [D:xxx]里的xxx表示这是一个词表, 词表统一放在dict.dic的文件中
> [num]是一个内置的词表, 无需提供, 他会专门匹配数字类型的值

4 .  填写词表文件dict.dic,其中包括词表[D:device], [D:model], [D:check]
词表表头均需以[D:xxx]开始命名
dict.dic文件如下
```
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
按照以上步骤就完成了自定义指令的操作, 按照上面的例子, 我们列举几个返回结果:
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
        "channel": 5
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

# 注：
num为系统函数，不需要单独提供

将intent.dic,dict.dic打包到appid命名的文件夹提交到baidu方即可
