# XSS

## pikachu靶场

### 1.get

输入\<script>alert(1)\</script>发现有字数限制

看源码发现在输入框标签了限制了20个字符

随便输入个a提交发现是get方法，直接在url上输入语句就弹框了



### 2.post

根据提示先用默认密码登录后台，发现输入框

尝试语句，发现没有字数限制，直接弹框

如果有字数限制的话，burp抓包再修改参数是一样的道理



### 3.存储型

是留言系统，会直接把输入的存储到服务器上

直接输入弹框语句，系统存入服务器后直接执行语句

弹框成功



### 4.DOM型

DOM概念：DOM文档就是一份XML文档，当有了DOM标准之后，DOM便将前端html代码化为一个树状结构，方便程序和脚本能够轻松的动态访问和更新这个树状结构的内容、结构以及样式，且不需要经过服务端。

分析源码发现是把输入的字符串直接拼接到 href标签里

因此用伪协议直接执行js代码

输入javascript:alert(1)

点击click直接弹框

代码：

```html
            <div id="xssd_main">
                <script>
                    function domxss(){
                        var str = document.getElementById("text").value;
                        document.getElementById("dom").innerHTML = "<a href='"+str+"'>what do you see?</a>";
                    }
                    //试试：'><img src="#" onmouseover="alert('xss')">
                    //试试：' onclick="alert('xss')">,闭合掉就行
                </script>
```



### 5.DOM型x

分析源码发现是过滤一些字符

```html
                    function domxss(){
                        var str = window.location.search;
                        var txss = decodeURIComponent(str.split("text=")[1]);
                        var xss = txss.replace(/\+/g,' ');
```

但我们使用伪协议不被过滤，因此同4



### 6.盲打

