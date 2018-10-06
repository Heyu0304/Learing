先在这里码一下，有一个开源的框架axion  
fetch()方法如下，在第二行参数里面设置传输参数，方法
fetch({usr},{header...}).then((response) =>(response.json()).then(function(json){
  })  
如果你要通过表单传递密码等值，可以这样做:
        let formdata = new FormData();
        formData.append('c','login');
        formData.append('username', this.state.userName);
        formData.append('password', this.state.passWord);
        formData.append('client', 'android');

        fetch(url,{
          method: 'post',
          body: formData,
          }).then(function (res) {
            return res.json();
            }).then(function (json) {
              if (json.code == "200") {
                console.log("232323233-----正确")
              }else if (json.code == "400") {
        console.log("2323232323------错了～")
      }
      })

作者：走走婷婷1215
链接：https://www.jianshu.com/p/5a33458e4a84
來源：简书  
# 不过这里要记一下东西，使用Fetch发送也很简单，配置三个参数。

fetch('some-url', options);
第一个参数是设置请求方法（如post、put或del），Fetch会自动设置方法为get。

第二个参数是设置头部。因为一般使用JSON数据格式，所以设置ContentType为application/json。

第三个参数是设置包含JSON内容的主体。因为JSON内容是必须的，所以当设置主体时会调用JSON.stringify。

实践中，post请求会像下面这样：

let content = {some: 'content'};

    // The actual fetch request
    fetch('some-url', {
    method: 'post',
    headers: {
      'Content-Type': 'application/json'
    },
        body: JSON.stringify(content)
    })

  因为fetch的Content-Type是 application/json模式的，和ajax不一样。ajax的'Content-Type'是  application/x-www-form-urlencoded .在Spring boot
  后端的传递中一般是@RequestParam("userName") String userName  是从header里面的取得参数。而fetch方法传输的json格式。所以，后端要加  @RequestBody Map map来取得参数。  
  # 关于axion看到官方的解决的方法，记一下.
  https://github.com/axios/axios/blob/master/README.md#using-applicationx-www-form-urlencoded-format

      import qs from 'qs';
      const data = { 'bar': 123 };
      const options = {
        method: 'POST',
        headers: { 'content-type': 'application/x-www-form-urlencoded' },
        data: qs.stringify(data),
        url,
      };
    axios(options)
