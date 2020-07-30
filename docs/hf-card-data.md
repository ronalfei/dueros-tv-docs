# hf运营数据对接文档

## hf运营数据推送接口

### 协 议

使用http协议、编码为utf-8

#### 请求方式

application/json POST

#### 请求地址

url: https://xiaodu.baidu.com/duertv/homefeed/push?code=\$code&t=\$timestamp $timestamp为当前时间戳, 每次请求都要带上来 $code的生成方式请联系度秘TV开发人员
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
| 1| template | String | 卡片模板 | 是 | 目前支持三种SINGLE,MULTITY_VERTICAL,MULTITY_HORIZONTAL,分别对应单图卡片、4张竖图卡片、3张横图卡片 |
| 2| partner | String | 合作商partner | 是 | 由度秘分配 |
| 3| background| String | 背景图 | 否 | 卡片的背景图 |
| 4| resourc_id| String | 卡片id | 是 | |
| 5| title| String | 卡片名称| 是 | 卡片名称 |
| 6| list_info| list| 资源列表 | 是 |[{"title": "", "link_click":"", "image_url": "", "width": 0, "height": 0, "index": 0},{...}], 具体见list_info说明 |

##### list_info 
| 字段名 | 字段类型 | 描述 |是否必填 | 备注 |
| list_info[].title| String| 标题 | 是 | |
| list_info[].link_click| String| object| 资源链接 | 是 |{"action": "", "applink": ""} 详见link_click说明|
| list_info[].image_url| String| 资源图片 | 是 | |
| list_info[].width| int| 图片宽度 | 否 | |
| list_info[].height| int| 图片高度 | 否 | |
| list_info[].index| int| 资源序号 | 否 | |

##### link_click
| 字段名 | 字段类型 | 描述 |是否必填 | 备注 |
| link_click[].action| String| app打开后的动作（apk内部自己定义） | 是 | |
| link_click[].applink| String| 要打开的apk的页面的地址，对应Open指令的app.url | 是 | |




#### 请求数据格式及示例

json格式

{"partner": "ireader", "background": "","resource_id": "1234", "title": "掌阅课外书漫画飙升榜", "template": "MULTITY_VERTICAL", "list_info": [{"title": "疯了！桂宝　5(开心卷)", "link_click": {"action": "android.intent.action.MAIN","applink": "ireader://com.zhangyue.read.edu.scheme/openurl?url=http%3A%2F%2Fk12.zhangyue.com%2Fzybk%2Faudio%2Fdetail%3Fid%3D30020138%26isPlay%3D0%26type%3D1%26reqType%3D26%26launch%3Dinside"}, "image_url": "http://book.img.ireader.com/idc_1/m_4,w_480,h_640,q_80/63621c27/group6/M00/3C/71/CmRaIVjAZeuEBnBKAAAAAHVfmps429758548.jpg?v=5gtBXf5P", "width": 0, "height": 0, "index": 0},{"title": "疯了！桂宝7·欢腾卷", "link_click": {"action": "android.intent.action.MAIN","applink": "ireader://com.zhangyue.read.edu.scheme/openurl?url=http%3A%2F%2Fk12.zhangyue.com%2Fzybk%2Faudio%2Fdetail%3Fid%3D30020138%26isPlay%3D0%26type%3D1%26reqType%3D26%26launch%3Dinside"}, "image_url": "http://book.img.ireader.com/idc_1/m_4,w_480,h_640,q_80/63621c27/group6/M00/3C/71/CmRaIVjAZeuEBnBKAAAAAHVfmps429758548.jpg?v=5gtBXf5P", "width": 0, "height": 0, "index": 0},{"title": "父与子", "link_click": {"action": "android.intent.action.MAIN","applink": "ireader://com.zhangyue.read.edu.scheme/openurl?url=http%3A%2F%2Fk12.zhangyue.com%2Fzybk%2Faudio%2Fdetail%3Fid%3D30020138%26isPlay%3D0%26type%3D1%26reqType%3D26%26launch%3Dinside"}, "image_url": "http://book.img.ireader.com/idc_1/m_4,w_480,h_640,q_80/63621c27/group6/M00/3C/71/CmRaIVjAZeuEBnBKAAAAAHVfmps429758548.jpg?v=5gtBXf5P", "width": 0, "height": 0, "index": 0},{"title": "爱上漫画：Q版美少女漫画技法一学就会", "link_click": {"action": "android.intent.action.MAIN","applink": "ireader://com.zhangyue.read.edu.scheme/openurl?url=http%3A%2F%2Fk12.zhangyue.com%2Fzybk%2Faudio%2Fdetail%3Fid%3D30020138%26isPlay%3D0%26type%3D1%26reqType%3D26%26launch%3Dinside"}, "image_url": "http://book.img.ireader.com/idc_1/m_4,w_480,h_640,q_80/63621c27/group6/M00/3C/71/CmRaIVjAZeuEBnBKAAAAAHVfmps429758548.jpg?v=5gtBXf5P", "width": 0, "height": 0, "index": 0}]}
