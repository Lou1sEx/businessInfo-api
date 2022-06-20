# 企业工商信息查询接口

企业工商信息接口(包含天眼查、企查查、爱企查、国家企业公示系统平台、快准)

接口文档(http://127.0.0.1:8081/docs)

tip:代理设置(158行更换)

项目运行  
  
`pip install requirements.txt -i https://pypi.doubanio.com/simple/`
  
` uvicorn 工商信息查询:app --host 0.0.0.0 --port 8081 --reload` 

docker 运行  
  
 `docker build -t businessinfo https://github.com/Litre-WU/businessInfo-api.git `  
   
 `docker run --name businessInfo -d -p 8081:8081 businessinfo`



#ZTESO接口示例
1.接口说明
1. 批量获取域名（/getDomains）
请求参数：entnames(string) 备注：以,为分割线。
请求实例：
```
var axios = require('axios');
var qs = require('qs');
var data = qs.stringify({
  'entnames': '深圳市农产品集团股份有限公司,深圳北斗卫星信息科技集团有限公司,深国际控股(深圳)有限公司,创维集团有限公司' 
});
var config = {
  method: 'post',
  url: 'http://49.235.105.117:8081/getDomains',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```

返回参数示例：
```
{
    "创维集团有限公司": [
        "skyworth.com"
    ],
    "深国际控股(深圳)有限公司": null,
    "深圳北斗卫星信息科技集团有限公司": null,
    "深圳市农产品集团股份有限公司": [
        "szap.com"
    ]
}

"公司名称"："域名"
```

2.域名搜索（/domain2all）
请求参数：domain(string) 一次只允许搜索一个，批量搜索回导致数据包过大增加服务器消耗。
请求示例：
```
var axios = require('axios');
var qs = require('qs');
var data = qs.stringify({
  'domain': 'ztems.com' 
});
var config = {
  method: 'post',
  url: 'http://49.235.105.117:8081/domain2all',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```


结果示例：
```
{
    "icp编号": "粤ICP备11108162号-3",
    "关联公司": {
        "xxx公司": "33%", `备注：百分比为投资占比即为占股比例`
    },
    "关联域名": [
        "ztems.com",
        "ztehotel.com.cn",
        "zte.com.cn",
        "zxingyun.com",
        "zte.net",
        "ztedevices.com",
        "ztedevice.com.cn",
        "ztedevice.com",
        "ztehotel.com"
    ],
    "域名归属公司/组织": "中兴通讯股份有限公司"
}
```

3.公司搜索（/company2all）
请求参数：entname(string) 一次只允许搜索一个，批量搜索回导致数据包过大增加服务器消耗。
请求示例：
```
var axios = require('axios');
var qs = require('qs');
var data = qs.stringify({
  'entname': '中兴通讯股份有限公司' 
});
var config = {
  method: 'post',
  url: 'http://49.235.105.117:8081/company2all',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```
结果示例

```
{
    "公司信息": "中兴通讯股份有限公司",
    "公司领导": {
        "丁建中": "董事会秘书",
        "吴君栋": "独立非执行董事",
        "夏小悦": "职工监事",
        "庄坚胜": "独立非执行董事",
        "徐子阳": "总裁,非独立董事",
        "方榕": "非独立董事",
        "李妙娜": "职工监事",
        "李步青": "非独立董事",
        "李自学": "董事长,法定代表人,非独立董事",
        "李莹": "执行副总裁,财务总监",
        "江密华": "股东代表监事",
        "王喜瑜": "执行副总裁",
        "蔡曼莉": "独立非执行董事",
        "诸为民": "非独立董事",
        "谢大雄": "监事会主席,职工监事",
        "谢峻石": "执行副总裁",
        "郝博": "股东代表监事",
        "顾军营": "执行副总裁,非独立董事"
    },
    "关联公司": {
        "上海中兴易联通讯股份有限公司": "100%",
    },
    "关联域名": [
        "ztedevice.com.cn",
        "ztedevices.com",
        "ztedevice.com",
        "zte.net",
        "ztehotel.net",
        "ztehotel.com",
        "zte.com.cn",
        "zxingyun.com",
        "ztehotel.com.cn",
        "ztems.com"
    ]
}
```
