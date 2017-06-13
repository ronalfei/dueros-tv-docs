## 通用识图接口文档
#### 整体逻辑
1. 用户发query：帮我看看这是什么水果
2. 服务端返回ImageRecognizer.StartRecognize的directive指令, 包含type参数：水果
    ```
    {
       "header": {
            "namespace":  "ImageRecognizer",
            "name":  "StartRecognize",
            "message_id": "message_id-1344"
        },
        "payload": {
            "type":"水果"
        }
    }
    ```
3. 客户端拍照（或者截图、让用户选图片）后发起ImageRecognizer.Recognize 的event, 包含type参数：水果，url参数：图片地址，message_id是步骤2中的message_id
```
{
    "device_event":{
        "header": {
            "namespace":  "ImageRecognizer",
            "name":  "Recognize",
            "message_id": "message_id-1344"
        },
        "payload": {
            "type":"水果", //可选
            "url":"http://f10.baidu.com/it/u=2640880481,1295783988&fm=72"
        }
    }
}
```
ps: 注意发起的请求是个event, 需要放在device_event里面

4. 度秘收到结果后返回resource数据
```
    "resource":{
        "face":{
            "resultData":[
                {
                    "location":{
                        "left":99,
                        "top":0,
                        "width":187,
                        "height":184
                    },
                    "name":"周杰伦",
                    "thumb":"http://10.94.243.177:8222/zhou.jpg",
                    "baikeUrl":"http://baike.baidu.com/item/%E5%91%A8%E6%9D%B0%E4%BC%A6/129156",
                    "description":"周杰伦（JayChou），1979年1月18日出生于台湾省新北市，中国台湾流行乐男歌手、音乐人、演员..."
                }
            ],
            "resultNum":1
        }

```
#### type可能的类型有如下四种
人脸识别:face
花卉识别: flower
logo识别: logo
汽车识别: car
