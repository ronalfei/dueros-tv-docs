# hf运营数据对接文档

## hf运营数据推送接口

### 协 议

使用http协议、编码为utf-8

#### 请求方式

application/json POST

#### 请求地址

url: https://xiaodu.baidu.com/duertv/data/pushplot?code=\$code&t=\$timestamp $timestamp为当前时间戳, 每次请求都要带上来 $code的生成方式请联系度秘TV开发人员
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
| 1| category | String | 分类 | 是 | 卡片的title |
| 2| partner| String | 合作商partner | 是 | 由度秘分配 |
| 3| resourc_id| String | 资源id | 是 | |
| 4| link_click| String | 资源链接| 是 | 资源链接 |
| 5| title| String| 资源名称 | 是 | |
| 6| image_url| String| 图片链接 | 是 | |
| 7| image_width| Int| 图片宽度 | 是 | |
| 8| image_height| Int| 图片高度 | 是 | |

#### 请求数据格式及示例

json格式，一次可以多条，但不能超过10条

{"partner": "ireader", "resource_id": 123, "category": "测试", "link_click": "http://www.baidu.com","title": "测试", "image_url": "test", "image_width": 100, "image_height": 100 }
