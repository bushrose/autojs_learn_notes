## 一、autojs介绍

---
1. **开发自动化、工作流小工具**

-  定时签到
-  自动收取蚂蚁森林能量
-  批量处理音频文件等

2.  **开发小应用**

- 开发web应用
- 开发app
- 开发小游戏等

3. **学习javascript和nodejs知识**

- 支持安装npm包

## 二、版本介绍
--- 

| 版本|介绍 | 是否有限制|
|----|----|----|
| autojs 4.1版本 | 免费的最后的开源版本 | 无限制 |
| autojs 7 pro | 收费 | 可以操作抖音、微信、qq等 |
| autojs 8 pro | 收费 | 限制抖音、微信、qq等大平台 |
| autojs 9 pro | 收费 | 限制抖音、微信、qq等大平台  |

## 三、实例分析
---

autojs版本：4.1

关注【产品经理不是经理】gzh，回复【autojs】即可下载4.1版本及打包插件。

打开朋友圈，采用布局层次分析即可查看朋友圈的布局结构如下：


```
ListView
    LinearLayout
        ImageView  头像
        TextView   昵称
        LinearLayout 
            android.view.view  说说内容(不是该控件说明是其他类型的说说)
        android.view.view   图片/视频
        FrameLayout        带视频的说说，含有帧布局控件，且只有一个兄弟组件为android.view.view
            RelativeLayout
        TextView           时间
        ImageView          点赞按钮
        TextView           点赞人员
        RelativeLayout
            android.view.view  评论内容
        RelativeLayout
            android.view.view  评论内容
```

## 四、完整代码

---

> 代码仅供学习交流，切勿用于非法用途

``` javascript
launchApp("微信")
//desc("微信").findOne().click();
id("f2s").className("android.widget.TextView").text("发现").findOne().parent().click();
id("iwg").indexInParent(0).findOne().click();
var i=1;

while(true){
    let j=1; //评论计数器
    // 先判断是否是朋友圈广告
    if(id("jtr").className("android.widget.RelativeLayout").exists()){
        let flag=true;
        while(flag){
            // 滚动朋友圈
            className("android.widget.ListView").findOne().scrollDown();
            sleep(3000);  
            var target=id("nq_").className("android.widget.LinearLayout").findOnce()
            if(target!=null){ flag=false}
        }
    }

    var shuoshuo=id("nq_").className("android.widget.LinearLayout").find();
    datas=[]
    shuoshuo.forEach(function(ele){
        log("=========第"+i+"条说说开始=========");
        data=[]
        data.push(i)
        ele.children().forEach(function(child,index){
            // log(child.children().size());
            if(index==1 && child.className()=="android.widget.TextView"){
                log("昵称："+ child.text());
                data.push(child.text())
            }
            if(index==2 && child.className()=="android.widget.LinearLayout"){
                if(child.children().size>1){
                    log("发表了其他分享链接类型的说说");
                    data.push('')
                }else{
                    content= child.children()[0].text() || child.children()[0].desc();
                    log("说说内容："+content)
                    data.push(content)
                }
            }

            if(child.id()=="com.tencent.mm:id/ju7" && child.className()=="android.widget.TextView"){
                // child.waitFor()
                log("点赞人员:"+child.text() || child.desc());
                data.push(child.text() || child.desc())
            }
            if(index>2 && child.className()=="android.widget.RelativeLayout" && child.children().size()>0){
                let comment=child.children()[0].desc();
                log("第"+j+"条评论："+comment);
                j+=1;
            }
    
    
        });
        log(data)
        datas.push(data)
        log("=========第"+i+"条说说结束=========");
        i+=1;
    });


    // 滚动朋友圈
    className("android.widget.ListView").findOne().scrollDown();
    sleep(3000);
}
```

