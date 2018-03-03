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

- HTML中导入share.min.css 和 share.min.js

      <!-- 禁用 google、设置分享的描述 -->
          <div class="social-share" data-disabled="google" data-description="Share.js - 一键分享到微博，QQ空间，腾讯微博，人人，豆瓣"></div>

       <!-- 设置微信二维码标题 -->
       <div class="social-share" data-wechat-qrcode-title="请打开微信扫一扫"></div>

       <!-- 针对特定站点使用不同的属性（title, url, description,image...） -->
       <div class="social-share" data-weibo-title="这个标题只有的分享到微博时有用，其它标题为全局标题" data-qq-title="分享到QQ时用此标题"></div>

       <!-- 使用: data-initialized="true" 标签或者 initialized 配置项来禁用自动生成icon功能。 -->
       <div class="social-share" data-initialized="true">
           <a href="#" class="social-share-icon icon-weibo"></a>
           <a href="#" class="social-share-icon icon-qq"></a>
           <a href="#" class="social-share-icon icon-qzone"></a>
       </div>

       <!-- 以上a标题会自动加上分享链接（a 标签必须带 icon-NAME 属性，不然分享链接不会自动加上）。 -->

       <!-- 如果你想在分享icon列表中内置一些元素，比如放一个收藏按钮在分享按钮的后面： -->
       <div class="social-share" data-mode="prepend">
           <a href="javascript:;" class="social-share-icon icon-heart"></a>
       </div>
       <!-- 这样，所有的分享图标就会创建在容器的内容前面，反之可以用 append 创建在容器内容后面，当然这是默认的，也不需要这么做。 -->

       <!-- 指定移动设备上显示的图标 -->
       <div class="share-component" data-mobile-sites="weibo,qq,qzone,tencent"></div>
       <!-- 当在手机上打开该页面的时候就只会显示这4个图标了。 -->
       
       
       // 展示所有配置可选， 通常默认就满足需求，不需在重新配置：(记得导入jquery)
       
      	//var $config = {
       //  ...
       // };

      // $('.social-share').share($config);


      // url                 : '', // 网址，默认使用 window.location.href
      // source              : '', // 来源（QQ空间会用到）, 默认读取head标签：<meta name="site" content="http://overtrue" />
      // title               : '', // 标题，默认读取 document.title 或者 <meta name="title" content="share.js" />
      // description         : '', // 描述, 默认读取head标签：<meta name="description" content="PHP弱类型的实现原理分析" />
      // image               : '', // 图片, 默认取网页中第一个img标签
      // sites               : ['qzone', 'qq', 'weibo','wechat', 'douban'], // 启用的站点
      // disabled            : ['google', 'facebook', 'twitter'], // 禁用的站点
      // wechatQrcodeTitle   : "微信扫一扫：分享", // 微信二维码提示文字
      // wechatQrcodeHelper  : '<p>微信里点“发现”，扫一下</p><p>二维码便可将本文分享至朋友圈。</p>',

