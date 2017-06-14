# 天气垂类

* Bot_id: duer_weather

* Query: 今天天气怎么样

* 返回结果样例:
```
{
    "result": {
        "nlu": {
            "domain": "duer_weather",
            "intent": "sys_weather",
            "slots": {
                "loc_city": "北京市",
                "loc_province": "北京市",
                "time": "2017-06-14,2017-06-14"
            }
        },
        "resource": {
            "type": "weather",
            "data": {
                "city": "北京",
                "current_temp": "34℃",
                "pm25": "112",
                "temp": "21℃~36℃",
                "time": "周三 06月14日",
                "weather": "晴",
                "weather_all": "晴，21℃~36℃，南风微风",
                "wind": "南风微风",
                "weather_info": [
                    {
                        "current_temp": "34℃",
                        "icon": "http://s1.bdstatic.com/r/www/aladdin/img/new_weath/bigicon/1.png",
                        "pm25": "112",
                        "pm_level": "轻度污染",
                        "temp": "21℃~36℃",
                        "time": "周三 06月14日",
                        "weather": "晴",
                        "wind": "南风微风"
                    },
                    {
                        "icon": "http://s1.bdstatic.com/r/www/aladdin/img/new_weath/icon/1.png",
                        "temp": "24℃~37℃",
                        "time": "周四 06月15日",
                        "weather": "晴",
                        "wind": "南风微风"
                    },
                    {
                        "icon": "http://s1.bdstatic.com/r/www/aladdin/img/new_weath/icon/5.png",
                        "temp": "25℃~35℃",
                        "time": "周五 06月16日",
                        "weather": "多云转阴",
                        "wind": "南风3-4级"
                    },
                    {
                        "icon": "http://s1.bdstatic.com/r/www/aladdin/img/new_weath/icon/3.png",
                        "temp": "25℃~34℃",
                        "time": "周六 06月17日",
                        "weather": "阴转多云",
                        "wind": "南风3-4级"
                    },
                    {
                        "icon": "http://s1.bdstatic.com/r/www/aladdin/img/new_weath/icon/5.png",
                        "temp": "22℃~33℃",
                        "time": "周日 06月18日",
                        "weather": "多云",
                        "wind": "南风微风"
                    }
                ]
            }
        },
        "bot_id": "duer_weather",
        "bot_meta": {
            "version": "1.0.0",
            "type": "其他",
            "description": "desc"
        },
        "views": [
            {
                "type": "list",
                "list": [
                    {
                        "title": "北京今天晴",
                        "summary": "实时：34℃\n温度：21℃~36℃\n风力：南风微风\n空气质量指数：112，轻度污染\n来源：中国天气网",
                        "url": "https://m.baidu.com/from=2001a/s?word=北京天气",
                        "image": "http://xiaodu.baidu.com/img/pic?pic_id=54239643"
                    }
                ]
            }
        ],
        "speech": {
            "type": "Text",
            "content": "北京今天高温黄色预警，晴，21℃~36℃，南风微风。空气质量指数为112，轻度污染。"
        }
    },
    "id": "1497421336_988gfo4uq",
    "logid": "14974213365844",
    "user_id": "E60D0298D473929BA4518CBD40471C95|0",
    "time": 1497421336,
    "cuid": null,
    "se_query": "今天天气怎么样",
    "msg": "ok",
    "status": 0
}
```

* ps: 对于天气垂类不同的问法, resource里返回的数据是一样的, 但对于speech里的content字段(语音播报字段)会有一些区分
* 比如:
    * "明天会下雨吗", speech里返回的就是: "北京明天不下雨，晴，24℃~37℃，南风微风"
