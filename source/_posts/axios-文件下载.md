---
title: axios 文件下载
date: 2019-04-30 15:23:49
categories: 
    - web前端
tags:
    - 小功能
---

上代码

```
downloadFile(url,params, callback){ // 下载文件
        const newUrl = params ? this.build(url, params) : url
        // let requestData = Object.assign({}, data, {
        //     accessToken: sessionStorage.getItem('accessToken')
        //   });
        axios.get(newUrl, {responseType: 'blob'}).then(resp => {
            let headers = resp.headers;
            let contentType = headers['content-type'];
      
            // console.log('响应头信息', headers);
            if (!resp.data) {
            //   console.error('响应异常：', resp);
              return false;
            } else {
            //   console.error('下载文件：', resp);
              const blob = new Blob([resp.data], {type: contentType});
      
              const contentDisposition = resp.headers['content-disposition'];
              let fileName = 'unknown';
              if (contentDisposition) {
                fileName = window.decodeURI(resp.headers['content-disposition'].split('=')[1]);
              }
            //   console.log('文件名称：', fileName);
            //   callback(blob, fileName)
              this.downFile(blob, fileName);
            }
        }).catch(function (error) {
            console.log(error);
        });
    }
    downFile(blob, fileName) {
        // 非IE下载
        if ('download' in document.createElement('a')) {
          let link = document.createElement('a');
          link.href = window.URL.createObjectURL(blob); // 创建下载的链接
          link.download = fileName; // 下载后文件名
          link.style.display = 'none';
          document.body.appendChild(link);
          link.click(); // 点击下载
          window.URL.revokeObjectURL(link.href); // 释放掉blob对象
          document.body.removeChild(link); // 下载完成移除元素
        } else {
          // IE10+下载
          window.navigator.msSaveBlob(blob, fileName);
        }
    }
```

[参考](https://www.jianshu.com/p/1a867612652c?tdsourcetag=s_pctim_aiomsg)