> **声明：文章仅用于学习交流，切勿用于非法用途。**

### 一、autojs版本

使用autojs版本4.1，其余版本对微信、qq、抖音有限制。

下载地址：关注【产品经理不是经理】gzh，回复【autojs】即可下载。

官方文档：https://pro.autojs.org/docs/zh/v8/

学习要点：熟悉对各种控件操作和布局分析

### 二、实例代码分析

通过autojs自带的布局分析可以查看控件信息，完成以下实例：
- 打开微信朋友圈

``` javascript
desc("微信").findOne().click();
id("f2s").className("android.widget.TextView").text("发现").findOne().parent().click();
id("iwg").indexInParent(0).findOne().click();
```

- 滚动朋友圈

```javascript
className("android.widget.ListView").findOne().scrollDown();
```

- 获取发说说的人员姓名

``` javascript
var nicknames=id("hg4").className("android.widget.TextView").find();
```

- 获取点赞按钮的位置，并点赞

``` javascript
 id("nh").find()[index].click();
 id("n3").findOne().click();
```

### 三、完整代码

```javascript
desc("微信").findOne().click();
id("f2s").className("android.widget.TextView").text("发现").findOne().parent().click();
id("iwg").indexInParent(0).findOne().click();
username="张三"
while(true){
    className("android.widget.ListView").findOne().scrollDown();
    sleep(3000);
    var nicknames=id("hg4").className("android.widget.TextView").find();
    if(nicknames.size()>0){
        nicknames.forEach(function(ele,index){
            if(ele.text()==username){
                toastLog("找到了"+ele.text());
                id("nh").find()[index].click();
                id("n3").findOne().click();
                toastLog("已给"+ele.text()+"点赞成功");
                exit();
            }else{
                toastLog("不是目标"+ele.text());
            }
        });

    }

}
```

### 四、总结

以上为简单示例代码，完成给指定好友点赞。大家可以发挥自己的脑洞，监测朋友圈信息，实现自动点赞等。