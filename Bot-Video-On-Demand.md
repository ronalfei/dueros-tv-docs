# 视频点播Bot返回结果

## 目录

* [Bot-id](#Bot-id:ai.dueros.bot.video_on_demand)
* [列表结果返回](#表结果返回)
* [详情结果返回](#详情结果返回)
* [带有播放意图的结果返回](#带有播放意图的结果返回)
* [检索结果为空的时候返回](#检索结果为空的时候返回)
* [directives字段解释](#directives字段解释)
* [NLU返回的结构](#NLU返回的结构)

## Bot-id:ai.dueros.bot.video_on_demand

##  列表结果返回

* Query样例: 我要看科幻电影
    * directives结果

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

* nlu结果

```
    {
         "domain": "FILM",
         "intent": "SEARCH_FILM",
         "slots": {
             "action_type": "搜索",
             "film_type": "科幻",
             "keyword": "科幻电影^500",
             "keyword_0": "科幻电影",
             "type": "电影"
         }
    }
```


## 详情结果返回
* Query样例: 我要看肖申克的救赎
    * directives 结果

```
"directives": [
            {
                "header": {
                    "message_id": "e0a6446c-52d1-427a-bb70-43cbc85eca83",
                    "name": "Render",
                    "namespace": "tv.view.detail"
                },
                "payload": {
                    "resource": {
                        "actors": "蒂姆·罗宾斯, 摩根·弗里曼, 鲍勃·冈顿, 摩根弗里曼, 鲍勃, 冈顿, 鲍勃冈顿, 威廉姆,  布朗, 克兰西布朗",
                        "area": "美国",
                        "category": "电影",
                        "description": "1946年，年青的银行家安迪被冤枉杀了他的妻子和其情人，这意味着他要在肖申克的监狱渡过余生。",
                        "director": "弗兰克·德拉邦特, 弗兰克, 德拉邦特, 弗兰克德拉邦特",
                        "era": "1994",
                        "poster_url": "http://res.tvxio.com/media/upload/20160420/upload/xskdjs480130625_poster.jpg",
                        "resource_id": "8adf4d3022ef5eac9b208504743bde03",
                        "resource_name": "肖申克的救赎",
                        "score": "9.60000038",
                        "thumb": "http://res.tvxio.com/media/upload/20160420/upload/xskdjs480130625_thumb.jpg",
                        "token": "233046",
                        "type": "剧情, 犯罪"
                    },
                    "tips": "为您找到肖申克的救赎"
                }
            }
```
* Query样例: 我要看锦绣未央

```
"directives": [
            {
                "header": {
                    "message_id": "e0a6446c-52d1-427a-bb70-43cbc85eca83",
                    "name": "Render",
                    "namespace": "tv.view.detail"
                },
                "payload": {
                    "resource": {
                        "actors": "唐嫣, 罗晋, 吴建豪, 毛晓彤, 李心艾",
                        "area": "内地",
                        "category": "电视剧",
                        "description": "南北朝期间，群雄逐鹿，烽烟四起，战事纷争不断。",
                        "director": "李慧珠",
                        "era": "2016",
                        "items": [
                            {
                                "episode": "1",
                                "item_id": "1",
                                "token": "436117"
                            },
                            {
                                "episode": "2",
                                "item_id": "2",
                                "token": "436120"
                            },
                            ......
                            {
                                "episode": "54",
                                "item_id": "54",
                                "token": "442526"
                            }
                        ],
                        "poster_url": "http://res.tvxio.com/media/upload/20160420/jinxiuweiyang161112_poster.jpg",
                        "resource_id": "ca435fbd5ac24a82ab2d2df81bda4098",
                        "resource_name": "锦绣未央",
                        "score": "4.80000019",
                        "thumb": "http://res.tvxio.com/media/upload/20160420/jinxiuweiyang161112_thumb.jpg",
                        "token": "717352",
                        "type": "剧情, 言情, 古装, 宫廷"
                    },
                    "tips": "为您找到锦绣未央"
                }
            }
        ],
```

*** ps:  电影返回的结果和电视剧的有少许差别, 电视剧会放回items这个字段, 而电影没有 ***

## 带有播放意图的结果返回

* Query样例: 播放欢乐颂第五集
    * directive 返回

```
"directives": [
    {
        "header": {
            "message_id": "1561de10-1cb8-4673-bec4-13fe0b971b06",
            "name": "Play",
            "namespace": "VideoPlayer"
        },
        "payload": {
            "resource": {
                "actors": "刘涛, 杨紫, 祖峰, 蒋欣, 王子文, 乔欣, 靳东",
                "area": "内地",
                "category": "电视剧",
                "description": "从外地来上海打拼的樊胜美（蒋欣饰）、关雎尔（乔欣饰）、邱莹莹（杨紫饰）三个女生合租一套房，",
                "director": "孔笙, 简川訸",
                "era": "2016",
                "items": [
                    {
                        "episode": "5",
                        "item_id": "5",
                        "token": "384112"
                    }
                ],
                "poster_url": "http://res.tvxio.com/media/upload/20160420/upload/20140922/huanlesong160418_poster.jpg",
                "resource_id": "e5d98324e6fb532b148548eba6841f61",
                "resource_name": "欢乐颂第一季",
                "score": "8.69999981",
                "thumb": "http://res.tvxio.com/media/upload/20160420/upload/20140922/huanlesong160418_thumb.jpg",
                "token": "696674",
                "type": "剧情, 爱情"
            },
            "tips": "为您找到电视剧综艺动漫欢乐颂"
        }
    }
],

```

* Query样例: 播放肖申克的救赎
    * 返回结果

```
"directives": [
    {
        "header": {
            "message_id": "1561de10-1cb8-4673-bec4-13fe0b971b06",
            "name": "Play",
            "namespace": "VideoPlayer"
        },
        "payload": {
            "resource": {
                "actors": "蒂姆·罗宾斯, 摩根·弗里曼, 鲍勃·冈顿, 威廉姆·赛德勒. ",
                "area": "美国",
                "category": "电影",
                "description": "1946年，年青的银行家安迪被冤枉杀了他的妻子和其情人.....！",
                "director": "弗兰克·德拉邦特, 弗兰克, 德拉邦特, 弗兰克德拉邦特",
                "era": "1994",
                "poster_url": "http://res.tvxio.com/media/upload/20160420/upload/xskdjs480130625_poster.jpg",
                "resource_id": "8adf4d3022ef5eac9b208504743bde03",
                "resource_name": "肖申克的救赎",
                "score": "9.60000038",
                "thumb": "http://res.tvxio.com/media/upload/20160420/upload/xskdjs480130625_thumb.jpg",
                "token": "233046",
                "type": "剧情, 犯罪"
            },
            "tips": "为您找到肖申克的救赎"
        }
    }
],
```

*ps: 同样, 电视剧会比电影类型的多items字段*

## 检索结果为空的时候返回

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

##  directives字段解释


字段| 含义
---|---
namespace| 指令命名空间, 包含4种 tv.view.text/ tv.view.list/ tv.view.detail/ VideoPlayer
name | 指令的名称 有两种: Render(针对视图渲染)/Play(针对播放器播放)
tips| 针对检索结果的简单解释
resource | 资源数组
resource.resource_id | 资源唯一id
resource.resource_name | 资源名称
resource.category | 资源类型, 主要为4大类, 电影/电视剧/综艺/动漫
resource.type | 资源子类型, 如: 科幻/恐怖/爱情等
resource.thumb| 资源显示所需的缩略图
resource.score| 该资源的网络评分
resource.description| 该资源的描述信息
resource.director| 该资源的导演
resource.actors| 该资源的演员, 用/分割
resource.era| 资源发布年代
resource.season| 如果该资源是一系列剧, 可能带这个参数
resource.token| 播放该剧的token(重要字段, 合作方用来和自己的播放应用就行对接的一个字段)
resource.poster_url| 海报图片的地址
resource.items| 资源为电视剧时, 会返回这个字段, 里面为每一集对应的id和token
resource.items.item_id| 电视剧某一集的id
resource.items.episode| 电视剧某集的序号
resource.items.token| 该集电视剧的播放token




## NLU返回的结构
* Domain: FILM
* Intent: SEARCH_FILM

```
Slots:{
    film:影视剧名
    type:影视剧类型
    tv_station:电视台
    series_film:系列电影名
    actor:演员
    director:导演
    presentor:主持人
    film_type:类型
    film_tag:标签
    descriptor:描述性内容
    film_area:地区
    film_language:语言
    time_slot:上映时间
    sort_type:排序方式
    action_type:动作类型
    is_free:是否免费播放
    online_watch:是否在线播放
    hd:是否高清播放
    release:是否正在热播
    pre_release:是否即将上映
    whdepart:第几部
    whepisode:第几集
    ----------以下为新增槽位----------
    whsuffix:后缀（部或集未知）
    person_name:人（类型未知）
    tv_role:角色
    tv_award:奖项
    tv_production_company:公司名
    keyword:query关键词
    keyword_*:query关键词
}
```
*Ps: 从whsuffix开始, 后面几个槽位为新增槽位*
