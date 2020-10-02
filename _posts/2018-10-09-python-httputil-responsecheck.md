
---
layout: post
title: "http response check"
date:   2018-10-9 21:16:52
categories: python
---

## 工具说明
功能：接口下发响应字段下发是否有缺失以及下发字段的类型是否正确
@param url     请求url
@param struct
## 伪代码说明业务流程
```
    判断是否存在
        判断是否数组
        	判断数组为空 && struct[item]是对象 && 该对象无""字段 && 该对象非空
    			遍历数组
            打印提示，遍历数组及序号
    				递归调用当前方法 入参数组元素和struct[item]    		
    	else：
            判断是否对象 && struct[item]是对象 && 该对象无""字段 && 该对象非空            
            else:
                打印相关提示    		
    	else:
    		目标类型为string
                判断是否匹配
                否：报错
            else：目标类型为int or long
                判断是否匹配
                否：报错
            else：
                将该情况打印    		
    else
    	报错
    	continue
```

## python实现源码
| 参数 | 名称 | 类型 | 说明 |
| ------ | ------ | ------ | ------ |
| @param | url | String | 请求url |
| @param | format | Json | 下发字段结构,如：{"a":"int,数量","b":"double,价格"}；参考sosoApi格式 |
| @return |   | Boolean | 响应是否匹配，以及console输出相关信息 |


