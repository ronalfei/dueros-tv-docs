# Bot-Tv-Control

## Bot-id
ai.dueros.bot.tv_control


## 设计原型

    {
    "header": {
        "namespace": "tv.xxx",
        "name": "Xxx"
    },
    "payload": {
        "extend":[]
    }
    }

1. 通过header中的namespace和name确定一种指令 
2. payload为指令附加的参数 
3. extend为扩展字段, 通常情况下都为空, 用户不需关心 
4. 尽可能使用全称,而不是简写 
5. namespace用小写和”.”分隔 
6. name采用首字母大写的驼峰命名法

## 详细指令列表
QUERY:开机
tv.system.command.TVOn

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"TVOn"
    },
    "payload":{
    "kv_extended":[] //kv_extended为额外信息的添加，做接口用，目前可忽略
    }
    }

QUERY:重启
tv.system.command.Restart

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Restart"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:关机
tv.system.command.TVOff

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"TVOff"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:休眠
tv.system.command.Sleep

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Sleep"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:唤醒
tv.system.command.Wake

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Wake"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:待机
**待机为V3新增功能**
tv.system.command.Wait

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Wait"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:音量增大
tv.system.volume.Up

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Up"
    },
    "payload":{
    "value":1,//这里有一个默认值
    "kv_extended":[]
    }
    }

QUERY:声音增大3
tv.system.volume.Up

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Up"
    },
    "payload":{
    "value":3,
    "kv_extended":[]
    }
    }

QUERY:音量降低
tv.system.volume.Down

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Down"
    },
    "payload":{
    "value":1,//默认值
    "kv_extended":[]
    }
    }

QUERY:音量减小3
tv.system.volume.Down

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Down"
    },
    "payload":{
    "value":3,
    "kv_extended":[]
    }
    }

QUERY:音量调为3
tv.system.volume.Set

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Set"
    },
    "payload":{
    #201706141139修改注释
    "value":3,//若query为音量调到最大/最小，均可支持，value值为max/min
    "kv_extended":[]
    }
    }

QUERY:静音
tv.system.volume.Mute

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Mute"
    },
    "payload":{
    "value":1,//静音和取消静音返回同header,槽位值不同
    "kv_extended":[]
    }
    }

QUERY:取消静音
tv.system.volume.Mute

    {
    "header":{
        "namespace":"tv.system.volume",
        "name":"Mute"
    },
    "payload":{
    "value":0,
    "kv_extended":[]
    }
    }
****注：V2版本静音与取消静音为Mute和Unmute两个意图，V3版本将其定位一个意图Mute，通过槽位值来区分是静音还是取消静音****
QUERY:增大对比度

        {
            "header":{
                "namespace":"tv.system.contrast",
                "name":"Up"
            },
            "payload":{
                 "value": 2,//填入默认值2
                "kv_extended":[

                ]
            }
        }
       
QUERY:降低对比度
```
    {
        "header":{
            "namespace":"tv.system.contrast",
            "name":"Down"
        },
        "payload":{
             "value": 2,//填入默认值2
            "kv_extended":[

            ]
        }
    }
```
QUERY:对比度
tv.system.command.Go

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Go"
    },
    "payload":{
        "name":"对比度",//这里可以解析对比度，设置，网络连接，首页，打开首页
        "kv_extended":[]
    }
    }

QUERY:调高亮度

    {
                "header":{
                    "namespace":"tv.system.light",
                    "name":"Up"
                },
                "payload":{
                    "value": 2,//填入默认值2
                    "kv_extended":[]
                }
            }

QUERY:降低亮度

    {
                "header":{
                    "namespace":"tv.system.light",
                    "name":"Down"
                },
                "payload":{
                     "value": 2,//填入默认值2
                    "kv_extended":[]
                }
            }

QUERY:退出
tv.system.command.Exit

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Exit"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:返回
tv.system.command.Back

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Back"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:退出设置
tv.system.command.Exit

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Exit"
    },
    "payload":{
        "name":"设置",
    "kv_extended":[]
    }
    }

QUERY:返回主页
tv.system.command.Go

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"Go"
    },
    "payload":{
        "name":"主页",
        "kv_extended":[]
    }
    }

QUERY:上一集
tv.player.control.Previous

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Previous"
    },
    "payload":{
    "kv_extended":[]
    }
    }
****注：上一页，下一页，上一集，下一集中V2版本均有返回槽位值value:1,V3版本中去掉****

QUERY:下一集
tv.player.control.Next

    {
        "header": {  
             "namespace": "tv.player.control", 
             "name": "Next", 
            },
        "payload": {   
             "extend": {}
         }
      } 

QUERY:第一集
tv.player.control.Episode

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Episode"
    },
    "payload":{
    "value":1,
    "kv_extended":[]
    }
    }

QUERY:暂停
tv.player.control.Pause

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Pause"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:取消暂停/播放/继续
tv.player.control.Continue

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Continue"
    },
    "payload":{
    "kv_extended":[]
    }
    }
***注：V2版本中将暂停、取消暂停归为Pause意图，通过槽位值来进行区分，V3版本改为Pause和Continue两个意图***

QUERY:快进
tv.player.control.FastForward
  
      {
            "header": {  
                  "namespace": "tv.player.control", 
                   "name": "FastForward", 
                },
            "payload": {   
                   "offset":30   //快进一次跨越的时间, 默认30秒
                   "extend": { }
                 }
            }

QUERY:快退
tv.player.control.BackForward

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"BackForward"
    },
    "payload":{
    "offset":30,//此处有个默认值，30s
    "kv_extended":[]
    }
    }

QUERY:从第一小时处开始播放
tv.player.control.Goto

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Goto"
    },
    "payload":{
    "offset":"3600",
    "kv_extended":[]
    }
    }

QUERY:3倍速播放
tv.player.control.Speed

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Speed"
    },
    "payload":{
    "value":3,
    "kv_extended":[]
    }
    }

QUERY:切换到3D模式
tv.player.control.Swith

    {
    "header":{
        "namespace":"tv.player.control",
        "name":"Swith"
    },
    "payload":{
        "name":"3d",
        "kv_extended":[]
    }
    }

QUERY:下一页
tv.system.page.Next

    {
    "header":{
        "namespace":"tv.system.page",
        "name":"Next"
    },
    "payload":{
    "kv_extended":[]
    }
    }

QUERY:上一页

    {
    "header": {
        "namespace": "tv.system.page",
        "name": "Previous"
    },
    "payload": {
        "extend": {}
    }
    }

QUERY:第一页

    {
    "header": {
        "namespace": "tv.system.page",
        "name": "Goto"
    },
    "payload": {
        "value":1,
        "extend": {}
    }
    }

QUERY:第二行第二个
tv.system.command.location

    {
    "header":{
        "namespace":"tv.system.command",
        "name":"location"
    },
    "payload":{
    "col":2,
    "row":2,
    "kv_extended":[]
    }
    }
QUERY:升级

```
    {
    "header":{
        "namespace":"tv.system.command",
        "name":"UpdateSystem"
    },
    "payload":{
    "kv_extended":[]
    }
    }
```
QUERY:系统升级


    {
    "header":{
        "namespace":"tv.system.command",
        "name":"UpdateSystem"
    },
    "payload":{
    "name":"系统",
    "kv_extended":[]
    }
    }

**

# 2017-06-24新增功能点

**

### 1、QUERY:倒数第二行最后一个 
tv.system.command.location
```
{
"header":{
    "namespace":"tv.system.command",
    "name":"location"
},
"payload":{
"re_col":1,
"re_row":2，//re_XXX表示倒数
"kv_extended":[]
}
}
```
### 2、QUERY:切换到第二个节目

tv.system.command.location
```
{
"header":{
    "namespace":"tv.system.command",
    "name":"location"
},
"payload":{
"num":2,
"kv_extended":[]
}
}
```

### 3、QUERY：跳过片头

tv.player.control.goto
```
{
"header":{
    "namespace":"tv.player.control",
    "name":"Goto"
},
"payload":{
"skip_title":"true"
"kv_extended":[]
}
}
```

### 4、QUERY：调整色彩度/色彩度

```
{
            "header":{
                "namespace":"tv.system.color",
                "name":"Adjust"
            },
            "payload":{
                "kv_extended":[]
            }
        }
   
```
### 4.1、QUERY：调整亮度/亮度
```
{
            "header":{
                "namespace":"tv.system.light",
                "name":"Adjust"
            },
            "payload":{
                "kv_extended":[]
            }
        }
```
### 4.2、QUERY：调整对比度/对比度
```
{
            "header":{
                "namespace":"tv.system.contrast,
                "name":"Adjust"
            },
            "payload":{
                "kv_extended":[]
            }
        }
```
* 注：2016-06-24前将query=“对比度”放在tv.system.command.Go中，此次修改将其拿出作为一个新的意图 

### 5、QUERY：色彩度增加30
```
{
            "header":{
                "namespace":"tv.system.color",
                "name":"Up"
            },
            "payload":{
                "value":30 //默认值为2
                "kv_extended":[]
            }
        }
```
### 6、QUERY：色彩度降低30
```
{
            "header":{
                "namespace":"tv.system.color",
                "name":"Down"
            },
            "payload":{
                "value":30 //默认值为2
                "kv_extended":[]
            }
        }
```
### 7、QUERY：色彩度增加到30
```
{
            "header":{
                "namespace":"tv.system.color",
                "name":"Set"
            },
            "payload":{
                "value":30,
                "kv_extended":[]
            }
        }
```
### 8、QUERY：对比度增加到30
```
{
            "header":{
                "namespace":"tv.system.contrast",
                "name":"Set"
            },
            "payload":{
                "value":30,
                "kv_extended":[]
            }
        }
```
### 9、QUERY：亮度增加到30
```
{
            "header":{
                "namespace":"tv.system.light",
                "name":"Set"
            },
            "payload":{
                "value":30,
                "kv_extended":[]
            }
        }
```
### 10、QUERY：调成TV模式/切换到HDMI1
```
 {
                "header":{
                    "namespace":"tv.system.command",
                    "name":"Signal"
                },
                "payload":{
                    "name":"tv", //可以是HDMI1，HDMI2，vga等
                    "kv_extended":[]
                }
            }
```
### 11、QUERY：截图
```
 {
                    "header":{
                        "namespace":"tv.system.command",
                        "name":"Cmd"
                    },
                    "payload":{
                        "name":"截图", //槽位值：截图，画面校正，清空内存，一键优化，                       
                        "kv_extended":[]
                    }
                }
```
### 12、QUERY：最后一页
```
{
    "header": {
        "namespace": "tv.system.page",
        "name": "Goto"
    },
    "payload": {
        "re_page_num":1,
        "extend": {}
    }
    }
```
### 13、QUERY：最后一集 
tv.player.control.Episode
```
{
"header":{
    "namespace":"tv.player.control",
    "name":"Episode"
},
"payload":{
"re_episode":1,
"kv_extended":[]
}
}
```




