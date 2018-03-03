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
           description: description
         }, function(){
           shareSuccess('facebook');  //分享成功回调
         });
         break;

         case "twitter":
         window.share.twitter.start({
             link: location.href,
             text: description
         }, function(){
            shareSuccess('twiter');  //分享成功回调
         });
         break;
         
         case "google":
         window.share.google.start({
           link: location.href,
           text: description + location.href
         }, function(){
            shareSuccess('google');  //分享成功回调
         });
         break;
         
         case "pinterest":
         window.share.pinterest.start({
           link: location.href,
           image: shareImg,
           text: description + location.href
         }, function(){
            shareSuccess('pinterest');  //分享成功回调
         })
       }
    }
    
    shareScucess: function(shareChannel){
       $.ajax({
         url: "成功回调的api地址"，
         type: "get/post",
         dataType: "json",
         data: {
           shareChannel: shareChannel || ''
         },
         success: function(res){
            if(res.code === 2){
              '代码块'
            }
         }
       })
    }
  
 - 现在说一下facebook的特殊性，facebook的分享只能抓取线上或者是预发布的描述，而且对于图片的抓取必须是线上抓取。
   它的抓取的方式是在 <head> 中：
   
       <meta property="og:type" content="product" />
       <meta property="og:url" content="www.baibu.com"/>
       <meta property="og:image" content="https://github.com/chenpenggood/share.js/blob/master/readImg/share.png?raw=true" />
       <meta property="og:description" content="this is share tool" />
       <meta property="og:site_name" content="share web" />
   
       <!-- <meta property="fb:app_id" content="100924140245002" /> 
        <meta property="fb:admins" content="100004662303870" /> -->
 
 附上: facebook抓取调试地址： https://developers.facebook.com/tools/debug/sharing/  
 
### 文件包share集合了jQuery分享插件jquery.share.js享到QQ、微信、微博、google、in、tweeter等

![img](https://github.com/chenpenggood/share.js/blob/master/readImg/share.min.png?raw=true) 
