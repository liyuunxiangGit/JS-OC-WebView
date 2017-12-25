# JS-OC-WebView


`WKWebView实现js交互`<br>

## 利用WKWebView  <br>  
* 1、实现js交互，`js调用native`,`native调用js`  <br>  
* 2、实现WebView中的`图片浏览`功能。点击可以`放大`。     <br>        
* 3、实现图片`长按进行保存`功能。                       <br>              
* 4、实现了webview中的文字`长按copy`功能。<br>  


![图片示意](https://github.com/liyuunxiangGit/JS-OC-WebView/blob/master/wkWebViewjs交互.gif)  


## JS-OC-WebView 代码实现详解  <br>
#### 1、首先创建控制器WKMianWebViewController
#### 2、然后控制器中`继承`如下类：

```
#import <WebKit/WebKit.h>
#import <AVFoundation/AVFoundation.h>
#import "WKWebViewJavascriptBridge.h"
#import "SDWebView.h"
```
#### 3、准备工作：
* 1、设置代理
```
WKNavigationDelegate,WKUIDelegate
```
* 2、在.h文件中
```
@property (strong, nonatomic)   SDWebView  *webView;
@property WKWebViewJavascriptBridge *webViewBridge;
```
#### 4、代码阶段：
* 1、viewDidLoad中`初始化`webView,实现[self initWKWebView]方法。方法如下：
```
- (void)initWKWebView
{
    WKWebViewConfiguration *configuration = [[WKWebViewConfiguration alloc] init];
    configuration.userContentController = [WKUserContentController new];
    
    WKPreferences *preferences = [WKPreferences new];
    preferences.javaScriptCanOpenWindowsAutomatically = YES;
    preferences.minimumFontSize = 30.0;
    configuration.preferences = preferences;
    
    SDWebView *webView = [[SDWebView alloc] initWithFrame:self.view.frame configuration:configuration];
    self.webView = webView;
    //如果是本地html，用下面方法：
    NSString *urlStr = [[NSBundle mainBundle] pathForResource:@"index.html" ofType:nil];
    NSString *localHtml = [NSString stringWithContentsOfFile:urlStr encoding:NSUTF8StringEncoding error:nil];
    NSURL *fileURL = [NSURL fileURLWithPath:urlStr];
    [webView loadHTMLString:localHtml baseURL:fileURL];
    //如果是网址，用下面的方法：
    //    [webView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:@"http://tbk.xxtapp.cn/test/unitActivity/hybrid.html?s=2"]]];
    webView.UIDelegate = self;
    [self.view addSubview:webView];
}
```
* 2、然后`初始化`webViewBridge并`注册代理`。
```
 _webViewBridge = [WKWebViewJavascriptBridge bridgeForWebView:self.webView];
 [_webViewBridge setWebViewDelegate:self.webView];
```
