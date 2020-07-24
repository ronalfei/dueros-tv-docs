# 直播数据对接文档
## 直播频道推送接口
### 协 议
使用http协议、编码为utf-8
#### 请求方式
application/json POST
#### 请求地址
url: http://duertv.baidu.com/duertv/data/pushchannel?code=\$code&t=\$timestamp 
\$timestamp为当前时间戳, 每次请求都要带上来
\$code的生成方式请联系度秘TV开发人员
#### 接口返回
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
|2001 | 字段未设置 | {"status":2001,"msg":"channel_code not set"} | 
|2002 | 字段值为空 | {"status":2002,"msg":"channel_code is null"} | 
|2003 | 字段值错误 | {"status":2003,"msg":"resource_status error"} | 
|2004 | 同一个请求中，partner不唯一 | {"status":2004,"msg":"partner is not unique"} |
|2005 | 记录数超过10条 | {"status":2005,"msg":"too many rows"} |
|2006 | channel_code不存在 | {"status":2006,"msg":"channel_code: xxx not exists"} |

#### 数据字段
|序号 |  字段名 | 字段类型 | 描述 |是否必填  | 备注 | 
|---|---|---|---|---|---|
| 1| channel_code | String | 频道码 | 是 | 由度秘基础频道数据指定的频道码 | 
| 2| channel_name| String | 频道名称 | 是 | 由度秘基础频道数据指定的频道名称 |
| 3| partner| String | 合作商partner | 是 | 由度秘分配 |
| 4| alias_name| String | 频道别名 | 否 | 多个别名以半角"/"分割，示例：cctv5/中央五台/中央体育频道 |
| 5| resource_status| int| 频道状态| 是 | 1正常 -1下线状态 |
| 6| extend| String| | 否 | |

#### 请求数据格式及示例
按照以下格式推送数据，一次可以多条，但不能超过10条

    {"channel_code":"cctv5","partner":"tcl2","channel_name":"cctv5","alias_name":"cctv5/中央五台/中央体育频道","resource_status":1}
    {"channel_code":"cctv1","partner":"tcl2","channel_name":"cctv1","alias_name":"cctv1/中央一台/中央电视台","resource_status":1}



## 直播频道节目推送接口
### 协 议
使用http协议、编码为utf-8
#### 请求方式
application/json POST
#### 请求地址
url: http://duertv.baidu.com/duertv/data/pushprogram?code=\$code&t=\$timestamp 
\$timestamp为当前时间戳, 每次请求都要带上来
\$code的生成方式请联系度秘TV开发人员
#### 接口返回
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
|2001 | 字段未设置 | {"status":2001,"msg":"channel_code not set"} | 
|2002 | 字段值为空 | {"status":2002,"msg":"channel_code is null"} | 
|2003 | 字段值错误 | {"status":2003,"msg":"resource_status error"} | 
|2004 | 同一个请求中，partner不唯一 | {"status":2004,"msg":"partner is not unique"} |

#### 数据字段
|序号 |  字段名 | 字段类型 | 描述 |是否必填  | 备注 | 
|---|---|---|---|---|---|
| 1| channel_code | String | 频道码 | 是 | 由度秘基础频道数据指定的频道码 | 
| 2| name| String | 节目名称 | 是 | 2018中国杯国际足球锦标赛半决赛| 
| 3| partner| String | 合作商partner | 是 | 由度秘分配 |
| 4| alias_name| String | 节目别名 | 否 | 多个别名以半角"/"分割，示例：2018中国杯/足球 |
| 6| resource_status| int| 节目状态| 是 | 1正常 -1下线状态 |
| 7| start_time| String| 节目开始时间| 是 | 年-月-日- 时:分:秒 格式，2018-03-25 00:05:00 |
| 8| end_time| String| 节目结束时间| 是 | 年-月-日- 时:分:秒 格式，2018-03-25 00:05:00 |
| 9| season| int| 节目季数| 否 | 示例 1表示第一季 |
| 10| episode| int| 节目集或者期数| 否 | 示例 1 表示第一集或者第一期 |
| 11| play_date| String| 节目播出日期| 是 | 示例 2018-03-25 |
| 12| program_id| String| 节目id| 是 | 示例 123 |
| 13| extend| String| | 否 | |

#### 请求数据格式及示例
按照以下格式推送数据，一次可以多条，但不能超过10条

    {"channel_code":"cctv5","partner":"tcl2","name":"2018中国杯国际足球锦标赛半决赛","alias_name":"2018中国杯/足球","start_time":"2018-03-25 00:05:00","duration":5400,"resource_status":1,"season":0,"episode":0,"play_date":"2018-03-25"}
    {"channel_code":"cctv5","partner":"tcl2","name":"2018年世界短道速滑锦标赛精选","alias_name":"","start_time":"2018-03-25 01:35:00","duration":6000,"resource_status":1,"season":0,"episode":0,"play_date":"2018-03-25"}

#### 示例代码

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


