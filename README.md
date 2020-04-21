## 主题开发步骤

> 推荐参考博客[https://www.cnblogs.com/yyhh/p/11058985.html](https://www.cnblogs.com/yyhh/p/11058985.html)
### 1. 新建主题文件夹
在 `themes` 目录下新建一个文件夹，作为主题文件夹。

### 2. 新建layout文件夹
* 在自己创建的主题文件夹下新建 `layout` 文件夹，并且在里面新建三个文件。`index.ejs` 、`layout.ejs` 、`post.ejs`
* 并在分别在三个文件里写上 `This is index` 、`This is layout` 与 `This is post` 的字样。用于测试。

### 3. 设置 utf-8 编码并引入index.ejs与post.ejs
编辑 `layout/post.ejs`，把内容修改如下：
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta charset="utf-8">
</head>
<body>
    Welcome to layout.ejs
    
    <%- include("index.ejs") %>

    <%- include("post.ejs") %>
</body>
</html>
```
访问 http://localhost:4000/ 查看效果。应该可以看到成功引入 `index.ejs` 和 `post.ejs`

### 4. 循环读取所有博客
编辑 `layout/post.ejs`，把内容修改如下：
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta charset="utf-8">
</head>
<body>
    Welcome to layout.ejs <br />
    <%- body %>
</body>
</html> 
```
编辑 `index.ejs`，把内容修改如下：
```html
Welcome to index.ejs<br />
<% site.posts.forEach(function(post){ %>
    <a href="/<%- post.path %>"><%- post.title %></a>
    <br />
<% }); %>
```
编辑 `layout/post.ejs`，把内容修改如下：
```html
Welcome to post.ejs <br />
<%- page.content %>
```

保存，访问。此时就可以发现基本已经完成博客的基本功能，即在首先显示所有博客的标题，通过点击就可以访问详细内容。

简单说来，
* 默认的主页是 `layout.ejs`;
* 这个例子中 `layout.ejs` 使用 `<%- body %>` 引入 `index.ejs`;
* `index.ejs` 提供访问 `post.ejs` 的路径;
* `post.ejs` 展示博客的详细内容。

### 5. 引用外部样式，正式开始编写主题
引用外部样式的方法即在 `layout/layout.ejs` 中引入即可，方法如下:
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta charset="utf-8">
    <%- css('css/main.css') %>
</head>
<body>
    Welcome to layout.ejs <br />
    <%- body %>
</body>
</html> 
```
