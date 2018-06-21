# 媒资数据schema及数据接口
    
[toc]

    
## 简介
    媒资数据是智能电视检索中重要的数据来源，由业务方提供，由于各业务方的数据格式差别很大，因此百度提供一份标准的schema用于接入不同业务方数据。该schema主要规定了：1、检索用字段；2、数据的层级依赖关系。
    
    数据接口是提供给业务方提交数据使用的。
    
## 版本
    version: 1.2
    
## 字段说明
	1、json中的value都是字符串类型，编码为utf-8。
	2、所有字段都必须提交，非必填字段请参照列表中说明填写

| 序号 | 字段 | 描述 | 字段类型 | 是否必填 |
|---|---|---|---|---|
|1 | id | 物料的id，全局唯一 | string | 必填
|2 | pid | <div>父id，如果是非剧集型数据(例如电影），那么pid=id；同一部剧集里的不同数据的pid要一致，不同剧集之间数据的pid不能相同，</div><div>比如亮剑电视剧中共有20集数据，每条数据的pid=345，那么任意其他数据的pid就不能再等于345了</div> | string | 必填
|3 | provider | 视频数据来源方 | string | 非必填，可以是空字符串
|4 | partner | 合作方、业务方 | string | 必填
|5 | resource_status | 上下线标识，1：上线；-1下线 | int | 必填
|6 | name | 影视或者资源名称 | string | 必填
|7 | serial_name | 系列名称 | string | 非必填，可以是空字符串
|8 | alias_name | 别名，用/分割 | string | 非必填，可以是空字符串
|9 | type | 类型（电影、电视剧、综艺、动漫、纪录片） | string | 必填
|10 | category | 分类，用/分割 | string | 非必填,可以是空字符串
|11 | source_type | 资源的其他分类字段（业务方可以根据自己需要将某个分类放入该字段） | string | 否，可以是空字符串
|12 | tag | 标签，用/分割 | string | 非必填,可以是空字符串
|13 | duration | 时长(秒) | int | 非必填，默认为0
|14 | season | 季、部 | int | 非必填,默认为1
|15 | total_episodes | 总集数 | int| 非必填，默认为1
|16 | episode | 当前集 | int| 非必填，默认为1
|17 | director | 导演，用/分割 | string | 非必填，可以为空串
|18 | actor | 演员， 用/分割 | string | 非必填，可以为空串
|19 | region | 地域，用/分割 | string | 非必填，可以为空串
|20 | release_date | 发布年代，精确到年,数据格式为yyyy-mm-dd或者yyyy,输出yyyy | int | 非必填
|21 | update_time | 更新时间， yyyyMMDD（示例：20171108） | int | 非必填
|22 | cost | 资费信息（付费/免费/vip） | string | 非必填，可以为空串，非空则三选一
|23 | hot | 热门值（业务方根据自己的计算公式计算该字段值，0~100） | int | 非必填，默认为0
|24 | weight | 权重，权重高的数据可能会被优先展示，0~100 | int |  非必填，默认为0
|25 | language | 语言，(中文/英文等) | string |非必填，可以是空串
|26 | definition | 清晰度，（超清、高清、流畅等） | string | 非必填，可以是空串
|27 | introduction | 视频简介 | string | 非必填，可以是空串
|28 | poster_url | 海报url | string | 必填
|29 | thumb_url | 海报缩略图url | string | 必填
|30 | token | 播放url或者是播放id | string | 必填
|31 | extend| 资源方自定义数据，不大于5000 | string | 非必填，可以是空串
|32 | score| 评分 | float | 非必填
    
### 名词解释
- 合辑页：id等于pid的记录。<b><font face="微软雅黑" color="#FF0000" >备注：所有数据，必须有一条合辑页记录（如果只有一条数据，如电影，可以使该数据pid=id即可，如果有分集数据，例如电视剧“人民的名义”，总共有52集，应该上传53条数据，其中合辑页id=pid）</font></b>

### 重要字段说明
    
 - id： 全局唯一，且不能等于0或-1；
 - pid： 剧集类数据依赖pid完成聚合操作，例如一部电数据有20集，那么应该有20条符合上述字段要求的json数据，每条数据的pid相同，并且不能和其他数据的id和pid重复；可以这么想象，剧集类数据存在一个虚拟json数据节点，该虚拟json数据是全集信息，而所有子集数据的pid等于该虚拟节点的id；
 - partner： 业务合作方的标识，例如联想业务就是"lenovo";
 - total_episodes:  针对剧集型数据，该字段表示总共有多少集，非剧集型数据该字段固定为1；
 - episode:  剧集型数据的该字段表示当前json数据是第多少集，如果是非剧集型，如电影，那么该字段固定为1；
 - hot： 热门值，业务方可根据自己需要提供该字段，例如通过播放量、评论数等换算成一个0~100的值；
 - weight： 权重，权重高的资源可能会被优先搜索出来，取值也是0~100。
 - duration：时长，单位秒，为了不影响merge效果，时长值必须定义真实有效值
    
    
## 数据示例
### 一条合法的非剧集型数据
电影《集结号》：

        {
            "id": "123",
            "pid": "123",
            "provider": "爱奇艺",
            "partner": "lenovo",
            "resource_status": "1",
            "name": "集结号",
            "serial_name": "",
            "alias_name": "Assembly",
            "type": "电影",
            "category": "战争/历史/动作",
            "source_type": "",
            "tag": "解放战争/谷子地/张涵予",
            "duration": "7080",
            "season": "",
            "total_episodes": "1",
            "episode": "1",
            "director": "冯小刚/王中磊",
            "actor": "张涵予/邓超/胡军",
            "region": "中国大陆",
            "release_date": "2006",
            "update_time": "20170227162314",
            "cost": "免费",
            "hot": "20",
            "weight": "30",
            "language": "中文",
            "definition": "超清",
            "introduction": "该片讲述了解放战争时期，连长谷子地在汶河岸执行掩护大部队撤退的任务；惨烈的战争中，全连除连长谷子地，47人全部阵亡；由于部队改了编号，九连牺牲的烈士们也被认定为失踪，谷子地开始了艰难的寻找，也为了探明当年集结号的真相",
            "poster_url": "www.xxx.jpg",
            "thumb_url": "www.xxx.jpg",
            "token": "www.xxx.mp4"
        }
        
    
### 一组合法的剧集型数据
    
电视剧《琅琊榜》第一、第二集：
    
        {
            "id": "456",
            "pid": "455",
            "provider": "爱奇艺",
            "partner": "lenovo",
            "resource_status": "1",
            "name": "琅琊榜 1",
            "serial_name": "琅琊榜",
            "alias_name": "Nirvana in Fire",
            "type": "电视剧",
            "category": "古装/言情/动作",
            "source_type": "",
            "tag": "麒麟才子/梅长苏",
            "duration": "2700",
            "season": "1",
            "total_episodes": "54",
            "episode": "1",
            "director": "孔笙/李雪",
            "actor": "胡歌/刘涛",
            "region": "中国大陆",
            "release_date": "2014",
            "update_time": "20170227162314",
            "cost": "免费",
            "hot": "60",
            "weight": "70",
            "language": "中文",
            "definition": "超清",
            "introduction": "梅长苏（胡歌饰）本远在江湖，却名动帝辇。江湖传言：“江左梅郎，麒麟之才，得之可得天下。”作为天下第一大帮“江左盟”的首领，梅长苏“梅郎”之名响誉江湖。然而，有着江湖至尊地位的梅长苏，却是一个病弱青年、弱不禁风，背负着十多年前巨大的冤案与血海深仇，就连身世背后也隐藏着巨大的秘密。",
            "poster_url": "www.xxx.jpg",
            "thumb_url": "www.xxx.jpg",
            "token": "www.xxx.mp4"
        }
    
    
----------

    
        {
            "id": "457",
            "pid": "455",
            "provider": "爱奇艺",
            "partner": "lenovo",
            "resource_status": "1",
            "name": "琅琊榜 2",
            "serial_name": "琅琊榜",
            "alias_name": "Nirvana in Fire",
            "type": "电视剧",
            "category": "古装/言情/动作",
            "source_type": "",
            "tag": "麒麟才子/梅长苏",
            "duration": "2700",
            "season": "1",
            "total_episodes": "54",
            "episode": "2",
            "director": "孔笙/李雪",
            "actor": "胡歌/刘涛",
            "region": "中国大陆",
            "release_date": "2014",
            "update_time": "20170227162314",
            "cost": "免费",
            "hot": "60",
            "weight": "70",
            "language": "中文",
            "definition": "超清",
            "introduction": "梅长苏（胡歌饰）本远在江湖，却名动帝辇。江湖传言：“江左梅郎，麒麟之才，得之可得天下。”作为天下第一大帮“江左盟”的首领，梅长苏“梅郎”之名响誉江湖。然而，有着江湖至尊地位的梅长苏，却是一个病弱青年、弱不禁风，背负着十多年前巨大的冤案与血海深仇，就连身世背后也隐藏着巨大的秘密。",
            "poster_url": "www.xxx.jpg",
            "thumb_url": "www.xxx.jpg",
            "token": "www.xxx.mp4"
        }
请注意电视剧子集id、pid的关系，动漫等剧集型数据和电视剧一样。
    
### 其他
    业务方在提供数据时需按照上述schema格式提供json数据，每条json数据30个字段需要完备，每个字段中的数据不要包含控制字符。如果某些字段缺失则填""，并且可能缺失的字段要提前告知百度。
    建议初次使用本schema适配业务数据的业务方先在离线的环境下转换若干条数据并发送给百度技术人员，百度技术人员帮助确认是否正确适配。
    
## 数据接口
### 增量数据接口一
#### 协议
使用http协议、编码为utf-8。
#### 请求方式
POST
#### 请求地址
url: http://s.xiaodu.baidu.com/duertv/data/push?code=\$code&t=\$timestamp
\$timestamp为当前时间戳, 每次请求都要带上来
\$code的生成方式请联系度秘TV开发人员


#### 请求数据
application/json
提交的数据为上文所述的schema格式json数据。
支持一次发送多条数据，建议一次发送10条以内，示例：

    {"id": 1249,"vod_id": "3922","parent_id": "3615","provider": "","partner": "test","resource_status": -1,"name": "英才发掘团 20160504","serial_name": "英才发掘团 2016","alias_name": "","type": "综艺","category": "访谈/真人秀","source_type": "","tag": "","duration": 3203,"season": 0,"total_episodes": 0,"episode": 20160504,"director": "","actor": "","region": "韩国/国外","release_date": "2016","update_time": "20170314","cost": "","hot": 0,"weight": 50,"language": "","definition": "","introduction": "《英才发掘团》是一档发掘人才的综艺娱乐节目。","poster_url": "http://192.168.80.45/poster/930.jpg","thumb_url": "","token": "http://192.168.80.39/otv/guangshi/1/70/44/00000002439/index.m3u8"}
    {"id": 1250,"pid":1249,"vod_id": "3923","parent_id": "2943","provider": "","partner": "test","resource_status": 1,"name": "长大成人 20160803","serial_name": "长大成人 2016","alias_name": "","type": "综艺","category": "真人秀","source_type": "","tag": "","duration": 2824,"season": 0,"total_episodes": 0,"episode": 20160803,"director": "","actor": "","region": "中国大陆","release_date": "2016","update_time": "20170314","cost": "","hot": 0,"weight": 50,"language": "","definition": "","introduction": "《长大成人》是由刘嘉玲作为发起人并全程监制的中国首档成长励志真人纪实节目。该节目中，刘嘉玲化身“成长导师”，带领七位来自全国各地的18岁少年，历经40天，克服重重困难，挑战攀登珠穆朗玛峰7028米，完成一次最高海拔的盛大成人礼！","poster_url": "http://192.168.80.45/poster/664.jpg","thumb_url": "","token": "http://192.168.80.39/otv/guangshi/8/EC/E2/00000002440/index.m3u8"}
    {"id": 1251,"pid":1249,"vod_id": "3920","parent_id": "3919","provider": "","partner": "test","resource_status": 1,"name": "那些年，我们一起追的女孩","serial_name": "那些年，我们一起追的女孩","alias_name": "","type": "电影","category": "爱情/喜剧","source_type": "","tag": "","duration": 6240,"season": 0,"total_episodes": 0,"episode": 1,"director": "九把刀","actor": "柯震东/陈妍希/敖犬/郝劭文","region": "中国台湾","release_date": "2012","update_time": "20170314","cost": "","hot": 0,"weight": 50,"language": "","definition": "","introduction": "成长，最残酷的部分就是，女孩永远比同年龄的男孩成熟。女孩的成熟，没有一个男孩招架得住。","poster_url": "http://192.168.80.45/poster/1015.jpg","thumb_url": "","token": "http://192.168.80.39/otv/guangshi/B/92/01/00000002437/naxienianwomenyiqizhuidenvhai.m3u8"}


    

#### 接口返回
如果数据正常接收，那么接口将返回：
    
    {
		    "status": 0,
		    "msg": "ok"
	}
    
如果数据非正常接收，那么接口返回：

|错误码 | 错误描述 | 示例 | 
|---|---|---|
|<font color="#ff628c">1000</font> | code错误 | {"status":1000,"msg":"error code"} | 
|1001 | 超时 | <span style="background-color: rgb(255, 255, 255);">{"status":</span>1001<span style="background-color: rgb(255, 255, 255);">,"msg":"</span>time expired<span style="background-color: rgb(255, 255, 255);">"}</span><br> | 
|1002 | 数据格式有错误 | <span style="background-color: rgb(255, 255, 255);">{"status":</span><span style="background-color: rgb(255, 255, 255);">1002</span><span style="background-color: rgb(255, 255, 255);">,"msg":"</span><span style="background-color: rgb(255, 255, 255);">data empty or not a valid json"}</span> | 
|2001 | 字段未设置 | {"status":2001,"msg":"pid not set id:1251 line:3"} | 
|2002 | 字段值为空 | {"status":2002,"msg":"pid is null id:1251 line:3"} | 
|2003 | 字段值错误 | {"status":2003,"msg":"resource_status error id:1251 line:3"} | 
|2004 | 同一个请求中，partner不唯一 | {"status":2004,"msg":"partner is not unique line:3"} | 
        

### 增量数据接口二
#### 协议
使用http协议、编码为utf-8。
#### 请求方式
POST
#### 请求地址
url: http://s.xiaodu.baidu.com/duertv/data/pushjson?code=\$code&t=\$timestamp
\$timestamp为当前时间戳, 每次请求都要带上来
\$code的生成方式请联系度秘TV开发人员


#### 请求数据
application/json
提交的数据为上文所述的schema格式json数据。
支持发送多条数据，建议每次发送10条以内，示例：

    [{"id":1249,"pid":1249,"vod_id":"3922","parent_id":"3615","provider":"","partner":"test","resource_status":1,"name":"\u82f1\u624d\u53d1\u6398\u56e2 20160504","serial_name":"\u82f1\u624d\u53d1\u6398\u56e2 2016","alias_name":"","type":"\u7efc\u827a","category":"\u8bbf\u8c08\/\u771f\u4eba\u79c0","source_type":"","tag":"","duration":3203,"season":0,"total_episodes":0,"episode":20160504,"director":"","actor":"","region":"\u97e9\u56fd\/\u56fd\u5916","release_date":"2016","update_time":"20170314","cost":"","hot":0,"weight":50,"language":"","definition":"","introduction":"\u300a\u82f1\u624d\u53d1\u6398\u56e2\u300b\u662f\u4e00\u6863\u53d1\u6398\u4eba\u624d\u7684\u7efc\u827a\u5a31\u4e50\u8282\u76ee\u3002","poster_url":"http:\/\/192.168.80.45\/poster\/930.jpg","thumb_url":"","token":"http:\/\/192.168.80.39\/otv\/guangshi\/1\/70\/44\/00000002439\/index.m3u8"},{"id":1250,"pid":1249,"vod_id":"3923","parent_id":"2943","provider":"","partner":"test","resource_status":1,"name":"\u957f\u5927\u6210\u4eba 20160803","serial_name":"\u957f\u5927\u6210\u4eba 2016","alias_name":"","type":"\u7efc\u827a","category":"\u771f\u4eba\u79c0","source_type":"","tag":"","duration":2824,"season":0,"total_episodes":0,"episode":20160803,"director":"","actor":"","region":"\u4e2d\u56fd\u5927\u9646","release_date":"2016","update_time":"20170314","cost":"","hot":0,"weight":50,"language":"","definition":"","introduction":"\u300a\u957f\u5927\u6210\u4eba\u300b\u662f\u7531\u5218\u5609\u73b2\u4f5c\u4e3a\u53d1\u8d77\u4eba\u5e76\u5168\u7a0b\u76d1\u5236\u7684\u4e2d\u56fd\u9996\u6863\u6210\u957f\u52b1\u5fd7\u771f\u4eba\u7eaa\u5b9e\u8282\u76ee\u3002\u8be5\u8282\u76ee\u4e2d\uff0c\u5218\u5609\u73b2\u5316\u8eab\u201c\u6210\u957f\u5bfc\u5e08\u201d\uff0c\u5e26\u9886\u4e03\u4f4d\u6765\u81ea\u5168\u56fd\u5404\u5730\u768418\u5c81\u5c11\u5e74\uff0c\u5386\u7ecf40\u5929\uff0c\u514b\u670d\u91cd\u91cd\u56f0\u96be\uff0c\u6311\u6218\u6500\u767b\u73e0\u7a46\u6717\u739b\u5cf07028\u7c73\uff0c\u5b8c\u6210\u4e00\u6b21\u6700\u9ad8\u6d77\u62d4\u7684\u76db\u5927\u6210\u4eba\u793c\uff01","poster_url":"http:\/\/192.168.80.45\/poster\/664.jpg","thumb_url":"","token":"http:\/\/192.168.80.39\/otv\/guangshi\/8\/EC\/E2\/00000002440\/index.m3u8"},{"id":1251,"pid":1249,"vod_id":"3920","parent_id":"3919","provider":"","partner":"test","resource_status":1,"name":"\u90a3\u4e9b\u5e74\uff0c\u6211\u4eec\u4e00\u8d77\u8ffd\u7684\u5973\u5b69","serial_name":"\u90a3\u4e9b\u5e74\uff0c\u6211\u4eec\u4e00\u8d77\u8ffd\u7684\u5973\u5b69","alias_name":"","type":"\u7535\u5f71","category":"\u7231\u60c5\/\u559c\u5267","source_type":"","tag":"","duration":6240,"season":0,"total_episodes":0,"episode":1,"director":"\u4e5d\u628a\u5200","actor":"\u67ef\u9707\u4e1c\/\u9648\u598d\u5e0c\/\u6556\u72ac\/\u90dd\u52ad\u6587","region":"\u4e2d\u56fd\u53f0\u6e7e","release_date":"2012","update_time":"20170314","cost":"","hot":0,"weight":50,"language":"","definition":"","introduction":"\u6210\u957f\uff0c\u6700\u6b8b\u9177\u7684\u90e8\u5206\u5c31\u662f\uff0c\u5973\u5b69\u6c38\u8fdc\u6bd4\u540c\u5e74\u9f84\u7684\u7537\u5b69\u6210\u719f\u3002\u5973\u5b69\u7684\u6210\u719f\uff0c\u6ca1\u6709\u4e00\u4e2a\u7537\u5b69\u62db\u67b6\u5f97\u4f4f\u3002","poster_url":"http:\/\/192.168.80.45\/poster\/1015.jpg","thumb_url":"","token":"http:\/\/192.168.80.39\/otv\/guangshi\/B\/92\/01\/00000002437\/naxienianwomenyiqizhuidenvhai.m3u8"}]

#### 接口返回
如果数据正常接收，那么接口将返回：
    
        {
            "code": 0,
            "msg": "ok"
        }
如果数据非正常接收，那么接口返回：  

|错误码 | 错误描述 | 示例 | 
|---|---|---|
|<font color="#ff628c">1000</font> | code错误 | {"status":1000,"msg":"error code"} | 
|1001 | 超时 | <span style="background-color: rgb(255, 255, 255);">{"status":</span>1001<span style="background-color: rgb(255, 255, 255);">,"msg":"</span>time expired<span style="background-color: rgb(255, 255, 255);">"}</span><br> | 
|1002 | 数据格式有错误 | <span style="background-color: rgb(255, 255, 255);">{"status":</span><span style="background-color: rgb(255, 255, 255);">1002</span><span style="background-color: rgb(255, 255, 255);">,"msg":"</span><span style="background-color: rgb(255, 255, 255);">data empty or not a valid json"}</span> | 
|2001 | 字段未设置 | {"status":2001,"msg":"pid not set id:1251 line:3"} | 
|2002 | 字段值为空 | {"status":2002,"msg":"pid is null id:1251 line:3"} | 
|2003 | 字段值错误 | {"status":2003,"msg":"resource_status error id:1251 line:3"} | 
|2004 | 同一个请求中，partner不唯一 | {"status":2004,"msg":"partner is not unique line:3"} | 

### php代码发送数据示例
```php
/**
     * @param string $data 需要发送的json格式媒资数据
     * @param        $url 接口地址
     *
     * @return string
     * 成功返回 {status: 0,msg: "ok"}
 **/
function post_($data = "", $url) {
	$opts = array(
        'http' => array(
            'method'  => "POST",
            'header'  => "Content-Type: application/json\r\n",
            'content' => $data,
			)
		);
		$context = stream_context_create($opts);
		$ret = file_get_contents($url, false, $context);
		return $ret;
	}
```
