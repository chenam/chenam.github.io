---
title: util
常: 用工具方法整理
date: 2019-04-10 16:24:25
tags:
    - javascript
---
### 常用工具方法

- 从url中获取参数
```
export default function(key){
	// 获取参数
  var url = window.location.search;
  // 正则筛选地址栏
  var reg = new RegExp("(^|&)"+ key +"=([^&]*)(&|$)");
  // 匹配目标参数
  var result = url.substr(1).match(reg);
  //返回参数值
  return result ? decodeURIComponent(result[2]) : null;
}
```
> 注意： 如果url上需要传入特殊字符，需要进行转码，encodeURIComponent()

- 时间格式化
```
/*
dateObj: date对象
format:你想要格式化的格式 如："'yyyy-MM-dd hh:mm:ss"
 */
export default function format(dateObj,format) {
    var date = {
       "M+": dateObj.getMonth() + 1,
       "d+": dateObj.getDate(),
       "h+": dateObj.getHours(),
       "m+": dateObj.getMinutes(),
       "s+": dateObj.getSeconds(),
       "q+": Math.floor((dateObj.getMonth() + 3) / 3),
       "S+": dateObj.getMilliseconds()
    };
    if (/(y+)/i.test(format)) {
       format = format.replace(RegExp.$1, (dateObj.getFullYear() + '').substr(4 - RegExp.$1.length));
    }
    for (var k in date) {
       if (new RegExp("(" + k + ")").test(format)) {
           format = format.replace(RegExp.$1, RegExp.$1.length == 1
              ? date[k] : ("00" + date[k]).substr(("" + date[k]).length));
       }
    }
    return format;
};
```