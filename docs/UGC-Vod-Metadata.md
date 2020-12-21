# UGC媒资数据对接文档
## 协 议
使用http/https协议、编码为utf-8
### 请求方式
application/json POST
### 请求地址
url: http://xiaodu.baidu.com/duertv/data/pushugc?code=\$code&t=\$timestamp 
\$timestamp为当前时间戳, 每次请求都要带上来
\$code的生成方式请联系度秘TV开发人员
### 接口返回
成功返回

    {
	    "status": 0,
	    "msg": "ok"
	｝
失败返回  

|错误码 | 错误描述 | 示例 | 
|---|---|---|
|1000 | code错误 | {"status":1000,"msg":"error code"} | 
|1001 | 超时 | {"status":1001,"msg":"time expired"} | 
|1002 | 数据格式有错误 | {"status":1002,"msg":"data empty or not a valid json"} | 
|2001 | 字段未设置 | {"status":2001,"msg":"name not set"} | 
|2002 | 字段值为空 | {"status":2002,"msg":"name is null"} | 
|2003 | 字段值错误 | {"status":2003,"msg":"resource_status error"} | 
|2004 | 同一个请求中，partner不唯一 | {"status":2004,"msg":"partner is not unique"} |
|2005 | 记录数超过10条 | {"status":2005,"msg":"too many rows"} |

### 数据字段
|序号 |  字段名 | 字段类型 | 描述 |是否必填  | 备注 | 
|---|---|---|---|---|---|
| 1| id | string | 资源id | 是 |  |
| 2| pid | string | 资源id | 是 | <div>父id，如果是非剧集型数据(例如电影），那么pid=id；同一部剧集里的不同数据的pid要一致，不同剧集之间数据的pid不能相同，</div><div>比如亮剑电视剧中共有20集数据，每条数据的pid=345，那么任意其他数据的pid就不能再等于345了</div> |
| 3| partner| string | 合作商partner | 是 | 由度秘分配 |
| 4| name| string | 资源名称 | 是 |  |
| 5| subtitle | string | 副标题 | 否 |  |
| 6| resource_status| int| 上下线状态| 是 | 1正常 -1下线状态 |
| 7| tag| string | 标签 | 是 | 多个tag以半角"/"分割，示例：生活/欢乐/搞笑 |
| 8| first_category| string | 一级分类 | 是 |  |
| 9| second_category| string | 二级分类 | 是 |  |
| 10| cover_url| string | 封面图 | 是 |  |
| 11| play_url| string | 播放地址 | 是 |  
| 12| duration| int | 时长 | 是 | 单位：秒 |
| 13| author_id| string | 作者id | 否 |  |
| 14| author| string | 作者 | 否 |  |
| 15| author_level| string | 作者级别 | 否 |  |
| 16| brief| string | 简介 | 否 |  |
| 17| episode| int | 集序号 | 否 |  |
| 18| total_episode | int | 总集数 | 否 |  |
| 19| preview_url_http | string | http的预览视频 | 否 |  |
| 20| preview_url_https | string | https的预览视频 | 否 |  |
| 21| preview_video_height | int | 预览视频高度 | 否 |  |
| 22| preview_video_width | int | 预览视频宽度 | 否 |  |
| 23| video_height | int | 视频高 | 否 |  |
| 24| video_width | int | 视频宽 | 否 |  |
| 25| video_size | int | 视频资源大小 | 否 |  |
| 26| video_info_ext | string | 视频扩展信息 | 否 |  |
| 27| video_score | double | 视频综合质量打分 | 否 |  |
| 28| comment_cnt | int | 评论数 | 否 |  |
| 29| like_cnt| int | 点赞数 | 否 |  |
| 30| collect_cnt | int | 收藏数 | 否 |  |
| 31| children_mode | string | 儿童模式级别 | 否 | 专属、可用、不可用 |
| 32| last_modify_time| int | 资源更新时间戳 | 否 | unix时间戳 |
| 33| create_time | string | 资源生成时间 | 否 | unix时间戳 |
| 34| cost | string | 付费标识 | 否 | 免费、付费、vip…… |
| 35| cost_info | string | 付费信息 | 否 | json，示例：{vip_info.xiaodu_vip=1} |
| 36| extend | string | 扩展信息 | 否 | |

### 请求数据格式及示例
按照以下格式推送数据，一次可以多条，但不能超过10条

    {"id": "39221","pid": "39221", "partner": "test","resource_status": 1,"name": "英才发掘团","play_url": "http://127.0.0.1/123456","cover_url":"http://192.168.80.45/poster/930.jpg","tag":"生活/欢乐/搞笑","first_category":"美食","duration":100}
    {"id": "39222","pid": "39222", "partner": "test","resource_status": 1,"name": "英才发掘团","play_url": "http://127.0.0.1/123456","cover_url":"http://192.168.80.45/poster/930.jpg","tag":"生活/欢乐/搞笑","first_category":"美食","duration":100}

### 示例代码

     /**
     * @param url
     * @param $data json格式的字符串
     * @return http结果
     */
    function curl_post($url, $data) {
        $header = array(
            'Content-Type: application/json; charset=utf-8',
        );
        $curl = curl_init();
        curl_setopt($curl, CURLOPT_TIMEOUT, 1);
        curl_setopt($curl, CURLOPT_URL, $url);
        curl_setopt($curl, CURLOPT_POST, 1);
        curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
        curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($curl, CURLOPT_HTTPHEADER, $header);
        $ret = curl_exec($curl);
        curl_close($curl);
        return $ret;

    }

    /**
     * @param $url
     * @param $data 推送数据,json格式的字符串
     *
     * @return string
     */
    function post($url, $data) {
        $opts = array(
            'http' => array(
                'method'  => "POST",
                'header'  => "Content-Type: application/json\r\n",
                'content' => $data,
                'timeout' => 1,
            )
        );
        $context = stream_context_create($opts);
        $ret = file_get_contents($url, false, $context);
        return $ret;
    }


