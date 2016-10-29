
### nodejs 入坑指南

####  创建一个最简单的项目
  
  >  安装nodejs
    mkdir express
接下来安装 Express
npm install -g express-generator@4

>创建一个工程
express helloworld
现在在express文件夹下就出现了helloworld项目

>安装依赖
cd helloworld
npm install

>备注：执行npm install命令会将package.json文件中 dependencies 依赖列表中,
即可自动安装依赖列表中所列出的所有模块。

>开启服务
执行npm start命令

>这样就可以在浏览器访问
http://localhost:3000/

>此时框架是找到views文件夹下的index.jade文件渲染到前台页面

>index.jade
extends layout

>block content
  h1= title
  p Welcome to #{title}


>改修改index.js文件的内容，将title改为Hello world.
var express = require('express');
var router = express.Router();
/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Hello world.' });
});
module.exports = router;
在命令行中，按ctrl+c关闭服务，重新执行npm start，看界面中的结果


#### 访问静态的html呢？很简单，下面一步步说来：

>首先，我们看app.js中有没有这句话
app.use(express.static(path.join(__dirname, 'public')));
有的话，则直接看下一步，没有就在app.js中添加这句话，记得添加后重启服务
接着，我们在项目的public文件夹下，新建一个html文件下（便于后期管理所有的静态页面），然后新建index.html,内容如下：

>\<!DOCTYPE html>
 \<html lang="en">
\<head>
\<meta charset="UTF-8">
\<title>demo</title>
\</head>
\<body>
\Hello world.
\</body>
\</html>

>这样在浏览器中输入下面的地址，就可以访问了。
http://localhost:3000/html/index.html

#### 读取json文件中的内容，提前绑定页面呢？（不依赖后端接口写好）

>为了方便项目管理，我们新建几个文件夹和对应的文件
json文件夹及其对应的index.json文件

* 在javascripts文件夹下新建index.js

>index.json
{
"code":"200",
"msg":"success"
}
index.js
fetch("../json/index.json").then(function(res) {
if (res.ok) {
res.json().then(function(data) {
  console.log(data);
});
} else {
console.log("Looks like the response wasn't perfect, got status", res.status);
}
}, function(e) {
console.log("Fetch failed!", e);
});

*在index.html中引入对应的文件
 ><!DOCTYPE html>
><html lang="en">
><head>
><meta charset="UTF-8">
><title>demo</title>
></head>
><body>
>Hello world.
><script src="../javascripts/index.js"></script>
></body>
></html>

>最后再打开访问http://localhost:3000/html/index.html
F12 打开控制台，我们可以看到打印出了我们想要的内容


