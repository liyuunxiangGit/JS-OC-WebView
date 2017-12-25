# JS-OC-WebView


`WKWebView实现js交互`<br>

## 利用WKWebView  <br>  
* 1、实现js交互，js调用native,native调用js  <br>  
* 2、实现WebView中的图片浏览功能。点击可以放大。     <br>        
* 3、实现图片长按进行保存功能。                       <br>              
* 4、实现了webview中的文字长按copy功能。<br>  


![图片示意](https://github.com/liyuunxiangGit/JS-OC-WebView/blob/master/wkWebViewjs交互.gif)  


## JS-OC-WebView 代码实现详解  <br>
* 1、首先创建控制器WKMianWebViewController
* 2、然后控制器中继承如下类：
** 
```
#import <WebKit/WebKit.h>
#import <AVFoundation/AVFoundation.h>
#import "WKWebViewJavascriptBridge.h"
#import "SDWebView.h"
```
