## 分享两个社交平台的分享文件

### 单独的share.min.js只针对Facebook、twitter、google、pinterest四种分享方法

- 一般用于国外网站的分享主流社交平台，文件容量极小

![img](https://github.com/chenpenggood/share.js/blob/master/readImg/share.png?raw=true) 

### 使用方法

  1. 在HTML中先写好标签，如下
  
  导入share.min.js
  
    <script src="../js/share.min.js"><script>

    <div class="share-msg">
        <p class="shareBtns share">
            <a data-share="facebook" class="share-facebook icon" href="javascript:;"></a>
            <a data-share="twitter" class="share-twitter icon" href="javascript:;"></a>
            <a data-share="google" class="share-google icon" href="javascript:;"></a>
            <a data-share="pinterest" class="share-pinterest icon" href="javascript:;"></a>
        </p>
    </div>
  
  PS: 每个分享的图片是自己根据设计图纸自定义的。
  
 在js文件中, （作者使用了jquery）
 
    $(document.body).on('click', 'shareBtns a', function(e){
       shareProcess($(this).attr('data-share'));
    });

    shareProcess: function(className){
       shareText = "Welcome share!",
       shareImg = "https://github.com/chenpenggood/share.js/blob/master/readImg/share.png?raw=true",
       twitterText = "share tool"，
       description: "this is a share tool"
       switch(className){
         case "facebook":
           window.share.fackbook.start({
             picture: shareImg,   //注意：新的facebook图片的分享有大变化，这里图片不能生效，下面会结束具体方法
             name: description,
             link: localtion.href， //注意：只能分享当前页面，否则fb抓取到指定页面的信息，这不是你想要的结果
             caption: "web name",
             description: descriptiton
           },function(){
             shareSuccess('facebook');  //分享成功回调
           });
           break;

         case "twitter":
         window.share.twitter.start({
             link: localtion.href,
             text: description
         })
       }
    }

### 文件包share集合了jQuery分享插件jquery.share.js享到QQ、微信、微博、google、in、tweeter等

![img](https://github.com/chenpenggood/share.js/blob/master/readImg/share.min.png?raw=true) 
