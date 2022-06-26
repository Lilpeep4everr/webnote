##简介
&emsp;&emsp;Ajax即Asynchronous Javascript And XML（异步JavaScript和XML）在 2005年被Jesse James Garrett提出的新术语，用来描述一种使用现有技术集合的‘新’方法，包括: HTML 或 XHTML, CSS, JavaScript, DOM, XML, XSLT, 以及最重要的XMLHttpRequest。使用Ajax技术网页应用能够快速地将增量更新呈现在用户界面上，而不需要重载（刷新）整个页面，这使得程序能够更快地回应用户的操作。

##优缺点
优点
*   可以无需刷新页面而与服务器端进行通信
*   允许你根据用户事件来更新部分页面内容

缺点
*   没有了浏览历史，不能退回
*   存在跨域问题（不同源）
*   SEO不友好，对爬虫也不友好（无法爬取）
*   

####需重点记忆ajax的promise封装
```
// 封装 ajax 请求：传入回调函数 success 和 fail
function ajax(url, success, fail) {
    var xmlhttp = new XMLHttpRequest();
    xmlhttp.open('GET', url);
    xmlhttp.send();
    xmlhttp.onreadystatechange = function () {
        if (xmlhttp.readyState === 4 && xmlhttp.status === 200) {
            success && success(xmlhttp.responseText);
        } else {
            fail && fail(new Error('接口请求失败'));
        }
    };
}

// Promise 封装接口1
function request1() {
    return new Promise((resolve, reject) => {
        ajax('https://www.baidu.com', (res) => {
            if (res.retCode == 201) {
                // 接口请求成功时调用：这里的 res 是接口1的返回结果
                resolve('request1 success' + res);
            } else {
                // 接口请求异常时调用异常
                reject('接口1请求失败');
            }
        });
    });
}

// Promise 封装接口2
function request2() {
    return new Promise((resolve, reject) => {
        ajax('https://www.jd.com', (res) => {
            if (res.retCode == 202) {
                // 这里的 res 是接口2的返回结果
                resolve('request2 success' + res);
            } else {
                reject('接口2请求失败');
            }
        });
    });
}

// Promise 封装接口3
function request3() {
    return new Promise((resolve, reject) => {
        ajax('https://www.taobao.com', (res) => {
            if (res.retCode == 203) {
                // 这里的 res 是接口3的返回结果
                resolve('request3 success' + res);
            } else {
                reject('接口3请求失败');
            }
        });
    });
}

// 先发起request1，等resolve后再发起request2；紧接着，等 request2有了 resolve之后，再发起 request3
request1()
    .then((res1) => {
        // 接口1请求成功
        console.log(res1);
        return request2();
    })
    .then((res2) => {
        // 接口2请求成功
        console.log(res2);
        return request3();
    })
    .then((res3) => {
        // 接口3请求成功
        console.log(res3);
    })
    .catch((err) => {
        // 从 reject中获取异常结果
        console.log(err);
    });
```