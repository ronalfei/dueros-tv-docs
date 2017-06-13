## 视频点播Bot返回结果

* Bot-id: ai.dueros.bot.video_on_demand

* 列表返回

```
{
"header": {
    "namespace": "tv.view.list",
    "name": "Render"
},
"payload": {
    "tips":"为您找到如下科幻电影",
    "resource": [{
        "resource_id": "123331",
        "resource_name": "美国队长",
        "category":"电影",
        "type": "科幻",
        "thumb": "http://aaa.jpg",
        "score": 7.5,
        "description": "美国队长史蒂夫·罗杰斯（克里斯·埃文斯 Chris Evans 饰）带领着全新组建的复仇者联盟，继续维护世界和平。"
        }, 
        {}{}{}....{}
    ]
}
}
```
* 详情返回
```
 {
        "header": {
          "namespace": "tv.view.detail",
          "message_id": "aca7dbe6-9822-4609-a6bf-9e712461bdd8",
          "name": "Render",
        },
        "payload": {
          "tips":"为您找到如下电影",
          "resource": {
            "category": "电影",
            "actors": "克里斯·埃文斯,小罗伯特·唐尼,斯嘉丽·约翰逊,塞巴斯蒂安·斯坦,伊丽莎白·奥尔森",
            "area": "美国",
            "type": "动作,科幻,惊悚",
            "description": "奥创纪元之后,全球政府联合颁布法令,管控超能力活动。对这条法令的不同态度,使复仇者阵营一分为二,钢铁侠和美国队长各据一方,其他复仇者则不得不做出自己的选择,最终引发前任盟友间的史诗大战。",
            "director": "乔·卢素,安东尼·卢素",
            "era": "2016",
            "poster_url": "http://imgsrc.baidu.com/forum/w=580/sign=81942e675543fbf2c52ca62b807fca1e/041716ce36d3d539f1c804ac3c87e950372ab0e1.jpg",
            "resource_id": "e403c600bf53b8630239d5a7470a7869",
            "resource_name": "美国队长3:内战",
            "token": "xxxxx"
          },
        }
```
* 带有播放意图的结果返回
```
      {
        "header": {
          "namespace": "VideoPlayer", 
          "name": "Play", 
        },
        "payload": {
        "tips": "为您找到如下电视剧",
          "resource": {
            "resource_id": "102_50451",
            "resource_name": "欢乐颂",
            "director": "孔笙",
            "type": "都市,言情",
            "category": "电视剧",
            "actors": "刘涛,蒋欣,王子文,杨紫",
            "era": "2016",
            "season": "1",
            "poster_url": "http://10.0.11.10/poster/15860.jpg",
            "episode" : 14,
            "item_id": "102_50452",
            "token": "xxxx"
            "description": "心怀梦想的大龄胡同公主樊胜美、大家闺秀闷骚文艺女...",
          }
            
        }
        
      }
     
```

* 检索结果为空的时候返回
```
      {
        "header": {
          "namespace": "tv.view.text",
          "name": "Render"
        },
        "payload": {
          "tips": "没能找到您想要的内容，不如试试其他影片吧"
        }
      }
```
