# Faq Bot

##FAQ功能介绍
FAQ提供常见的问题与解答，以一问一答的形式展示，需要合作方提供健康合法的问答数据集。合作方需要确认该数据集资源是否需要授权，需要授权则只允许部分端访问，其它端无权限访问或需要付费才能访问；不需要授权则免费开放给所有端。
合作方提供的每一个问答数据集资源对应一个经过百度审核的bot名称，同时需要满足下面介绍的数据格式，百度会在合作方提供数据集资源后的两个星期内上线该功能。
## 提供的数据格式
资源方提供的问答数据集文件每行存储一条纪录，一条记录即表示一个问答环节，每条记录均为json格式，数据中的question即为问题描述，answer为问题答案，同时json数据中不能存在空格，下面是json格式的字段说明以及示例：
**字段说明**
|字段  | 说明 | 是否必须 | 示例 | 
|---|---|---|---|
|vendor | 资源方标识码（百度分配） | 是 | 2 | 
|source | 资源方域名 | 否 | citicguoanbn | 
|category | 策略 | 否 | baike | 
|domain | 域 | 是 | faq |
|intent | 意图 | 是 | faq |
|question | 问题描述 | 是 | “夕” | 
|answer | 问题文本答案 | 是 | “xi ①傍晚；日落的时候(跟“朝zhāo”相对)：夕阳朝夕相处危在旦夕。 ②夜晚：前夕除夕七夕。” | 
|voice | 问题声音答案 | 否 | “夕 ①傍晚；日落的时候(跟“朝zhāo”相对)：夕阳朝夕相处危在旦夕。 ②夜晚：前夕除夕七夕。” | 
**资源文件内容**
```javascript
{
    "vendor": "3",
    "source": "citicguoanbn",
    "category": "baike",
    "domain": "faq",
    "intent": "faq",
    "question": "夕",
    "answer": "xī ①傍晚；日落的时候(跟“朝zhāo”相对)：夕阳|朝夕相处|危在旦夕。 ②夜晚：前夕|除夕|七夕。",
    "voice": "夕 ①傍晚；日落的时候(跟“朝zhāo”相对)：夕阳|朝夕相处|危在旦夕。 ②夜晚：前夕|除夕|七夕。"
}
{
    "vendor": "3",
    "source": "citicguoanbn",
    "category": "baike",
    "domain": "faq",
    "intent": "faq",
    "question": "希望小学",
    "answer": "xīwàng xiǎoxué 由希望工程捐资兴建的小学。",
    "voice": "希望小学 xiǎoxué 由希望工程捐资兴建的小学。"
}
{
    "vendor": "3",
    "source": "citicguoanbn",
    "category": "baike",
    "domain": "faq",
    "intent": "faq",
    "question": "细雨",
    "answer": "xìyǔ 很小的雨：牛毛细雨|细雨霏霏|细雨如丝。",
    "voice": "细雨 很小的雨：牛毛细雨|细雨霏霏|细雨如丝。"
}
```

**注意**：vendor字段找PM申请，domain以及intent字段均固定为faq。

**当前,合作方按照上述格式提交文件给到对应的PM即可**

