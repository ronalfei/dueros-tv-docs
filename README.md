# TV场景下能接入的BOT及其接口说明
[TOC]


## Bot-TV-Control (电视通用控制指令BOT)
[详细文档](Bot-TV-Control.md)

* ChangeLog
    * 详见文档中的黑体部分



## Bot-Image-Recognition (图像识别)
[详细文档](Bot-Image-Recognition.md)

* ChangeLog
    * 整体的方式有变动, 逻辑上修改得更加友好, 对接时需直接参考[详细文档]



## Bot-TV-Live (电视直播)
[详细文档](Bot-TV-Live.md)

* ChangeLog
    * 1. Bot-id的变化: smart_tv -> ai.dueros.bot.tv_live
    * 2. nlu 结果的变化
        * domain: COMMAND -> tv.live 
        * intent: channel.open -> tv.live.channel.search
        * slots: 删除了channel_code字段
    * 3. directives中的header有变化, payload无变化
        * namespace: tv.system.channel -> tv.command.live
        * name: Open -> SwitchChannel


## Bot-Video-On-Demand (视频点播服务<新>)
[详细文档](Bot-Video-On-Demand.md)

* ChangeLog
    * 1. Bot-id的变化: smart_tv -> ai.dueros.bot.video_on_demand
    * 2. Nlu的变化: 新增keyword关键字, 可用来做检索, 新增person_name字段, 当无法识别是演员还是导演的时候, 会出现改字段.
    * 3. directive中列表渲染指令的header无变化, payload里有变化
        * payload里的ott_res -> resource
        * payload.category与payload.type调了个顺序, 即: category表示一级分类, type表示二级分类
        * 增加score字段, 描述该影片的得分
        * 增加token字段, 可用来做播放的钥匙
        * 增加tips字段, 提示用户这批内容的属性
    * 4. directive中详情信息指令渲染header无变化, payload里有变化
        * category与type调了个顺序, 即: category表示一级分类, type表示二级分类
        * 增加了地域:area, 得分:score, 以及token字段
        * items里增加了episode
        * 增加tips字段
    * 5. 新增一种directive类型, namespace为VideoPlayer, name为Play, 意为告诉终端, 用户想直接播放该影片
        * 具体描述可以参见: [带有意图播放的结果](/Bot-Video-On-Demand.md#%E5%B8%A6%E6%9C%89%E6%92%AD%E6%94%BE%E6%84%8F%E5%9B%BE%E7%9A%84%E7%BB%93%E6%9E%9C%E8%BF%94%E5%9B%9E)


## Bot-Ui-Voice-Interaction (场景注册)
[详细文档](https://github.com/dueros/dumi_doc/blob/master/doc/directives/UiControl.md)


## Bot-TV-custom-command (通用自定义指令)
[详细文档](Bot-TV-Custom-Command.md)


## Bot-App-Launcher (应用控制)
[详细文档](https://github.com/dueros/dumi_doc/blob/master/doc/bot/app_launcher.md)


## Bot-Audio-Music (音乐垂类)
[详细文档](https://github.com/dueros/dumi_doc/blob/master/doc/bot/audio_music.md)


## Bot-Audio-News (新闻垂类)
[详细文档](https://github.com/dueros/dumi_doc/blob/master/doc/bot/audio_news.md)


## Bot-Duer-weather (天气)
[详细文档](Bot-Duer-Weather.md)


## Bot-Aries-Genaral (通用信息)
[详细文档](Bot-Aries-General.md)


## Bot-Audio-Joke (音频笑话垂类)
[详细文档](Bot-Audio-Joke.md)


## Bot-Text-Joke (文本笑话垂类)
[详细文档](Bot-Text-Joke.md)


