# 剧情数据对接文档

## 剧情数据推送接口

### 协 议

使用http协议、编码为utf-8

#### 请求方式

application/json POST

#### 请求地址

url: http://duertv.baidu.com/duertv/data/pushplot?code=\$code&t=\$timestamp $timestamp为当前时间戳, 每次请求都要带上来 $code的生成方式请联系度秘TV开发人员
#### 接口返回

成功返回

{

"status": 0,

"msg": "ok"

｝

失败返回

| 错误码 | 错误描述 | 示例 |
|---|---|---|
|1000 | code错误 | {"status":1000,"msg":"error code"} |
|1001 | 超时 | {"status":1001,"msg":"time expired"} |
|1002 | 数据格式有错误 | {"status":1002,"msg":"data empty or not a valid json"} |
|2001 | 字段未设置 | {"status":2001,"msg":"vod_id not set"} |
|2002 | 字段值为空 | {"status":2002,"msg":"vod_code is null"} |
|2003 | 字段值错误 | {"status":2003,"msg":"type error"} |
|2004 | 同一个请求中，partner不唯一 | {"status":2004,"msg":"partner is not unique"} |
|2005 | 记录数超过10条 | {"status":2005,"msg":"too many rows"} |

#### 数据字段

|序号 | 字段名 | 字段类型 | 描述 |是否必填 | 备注 |
|---|---|---|---|---|---|
| 1| vod_id | String | vod码 | 是 | 厂商提供的vod_id |
| 2| partner| String | 合作商partner | 是 | 由度秘分配 |
| 3| episode| int | 当前集 | 是 | |
| 4| plot_type| string | 剧情类型| 是 | 共4种类型，剧情类型是plot_fragment，镜头类型是person_appearance，台词类型是actor_lines，只看XX数据类型是specific_cast_footage |
| 5| plot_info| String| 剧情信息 | 是 | |
| 6| plot_play_time| int| 剧情时间，单位秒 | 是 | |

#### 请求数据格式及示例

json格式，一次可以多条，但不能超过10条

{"vod_id":"cmv67rzhrf5s5r3","partner":"tcl2","episode":20,"plot_type":"plot_fragment","plot_info":"昔日同胞今反目苍梧之巅决胜负","plot_play_time":1789}
{"vod_id":"ulilbfmznfgweqg_8Pc3ExVaQYC","partner":"tcl2","episode":13,"plot_type":"person_appearance","plot_info":"方圆金铭出场","plot_play_time":321}
