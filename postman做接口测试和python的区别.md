> postman是一个做接口测试的工具，它是谷歌公司的，可谓是根正苗红的大家族。在接口测试领域和它拼的一个手指头也能数得出来。POSTMAN本只是Chrome的一个插件工具，后来谷歌老爹看着小家伙越来越受测试工程师的喜爱，名气越来越大，便做了一个决定给了它一个正名，承认postman是谷歌成员的身份。postman不在是寄生在Chrome浏览器的一个插件了。现在的postman是个真男人了，有了自己的APP，不再寄人篱下后也混越好。目前只有同是名门的jmeter可以和他有一拼。jmeter是何许人也？	Apache你一定听说过。它就来自Apache家族。
>
> 

postman能做的事情有什么。无非就是遵循接口测试的原理罢了。



接口测试的原理就是你发一个请求给服务器，服务器返回一个响应报文。然后我们判断这个响应报文的数据是否和预期的一样。这个预期看需求文档就行了。



其实我们用python代码也能实现这个过程。无非就是你拿着接口（实质就是个URL），在URL里面放上你要请求的数据对应的参数就行了。比如下面这个水质量的接口文档：



```
接口地址：http://web.juhe.cn:8080/environment/water/river
返回格式：json
请求方式：get
请求示例：http://web.juhe.cn:8080/environment/water/river?river=流域名称&key=您申请的APPKEY值
接口备注：有的监测站点没有总有机碳监测数据
```



这个接口url为`http://web.juhe.cn:8080/environment/water/river`,但是如果你要查询<kbd>长江流域</kbd>的水质量，就要在这个接口URL地址中加入参数<kbd>?river=流域名称&key=您申请的APPKEY值</kbd>。然后再用<kbd>get</kbd>方法进行请求就行了。



postman的作用就是把这个过程图形化了，操作也就更简单了。postman很简单，我就不过做笔记了。今天用python代码做一下。



```javas
import requests

data = {
    "times": 100, # 请求次数
    "method": "POST", # GET or POST
    "url": "http://xxx.com/xxx",
    "cookies": {
        "PHPSESSID": "cnguud4r1hmn3passs906odp21"
    },
    "proxy": {
        # 代理设置
    },
    "header": {
        "Content-Type": "application/json", # application/x-www-form-urlencoded
        "user-agent": "python-mock/0.0.1",
        "token": ""
    },
    "body": {
        # 请求参数
    }
}

index = 1
while index <= data["times"]:
    if data["method"] == "GET":
        response = requests.get(
            data["url"], params=data["body"], headers=data["header"], 		   	cookies=data["cookies"], proxies=data["proxy"])
    elif data["header"]["Content-Type"] == "application/json":
        response = requests.post(
            data["url"], json=data["body"], headers=data["header"], cookies=data["cookies"], proxies=data["proxy"])
    else :
        response = requests.post(
            data["url"], data=data["body"], headers=data["header"], cookies=data["cookies"], proxies=data["proxy"])

    if response.status_code == 200:
        result = response.content.decode('utf-8')
    else:
        result = "访问失败"
    print("第 %s 次执行：%s" % (index, result))
    print()
    index += 1
```

#Content-Type:application/json
#Content-Type:multipart/form-data

