# BAWKWebView
[![BAHome Team Name](https://img.shields.io/badge/Team-BAHome-brightgreen.svg?style=flat)](https://github.com/BAHome "BAHome Team")
![](https://img.shields.io/badge/platform-iOS-red.svg) ![](https://img.shields.io/badge/language-Objective--C-orange.svg) 
![](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg) 
![](https://img.shields.io/cocoapods/v/BAWKWebView.svg?style=flat) ![](https://img.shields.io/cocoapods/dt/BAWKWebView.svg
)  [![](https://img.shields.io/badge/微博-博爱1616-red.svg)](http://weibo.com/538298123)

## 1、功能及简介
* 1、用分类封装 WKWebView，代码无任何侵入更改 <br>
* 2、用 block 方式实现所需代理回调，更加方便，代码更简洁
* 3、一行代码搞定 request、URL、URLString、本地 HTML文件、HTMLString等请求
* 4、一个 block 搞定 title、progress、currentURL、当前网页的高度等等所需
* 5、有博爱封装好的 BAWebViewController 可以直接使用，也可以参考自定义浏览器【参考demo】
* 6、WKWebView 自定义 request post 数据到 JS（使用分类）

## 2、图片示例
![BAWKWebView](https://github.com/BAHome/BAWKWebView/blob/master/Images/BAWKWebView.gif)

## 3、安装、导入示例和源码地址
* 1、pod 导入【最新版本：![](https://img.shields.io/cocoapods/v/BAWKWebView.svg?style=flat)】： <br>
 `pod 'BAWKWebView'` <br>
如果发现 `pod search BAWKWebView` 搜索出来的不是最新版本，需要在终端执行 cd 转换文件路径命令退回到 desktop，然后执行 `pod setup` 命令更新本地spec缓存（可能需要几分钟），然后再搜索就可以了。<br>
具体步骤：
  - pod setup : 初始化
  - pod repo update : 更新仓库
  - pod search BAWKWebView
* 2、文件夹拖入：下载demo，把 BAWKWebView 文件夹拖入项目即可，<br>
* 3、导入头文件：<br>
`  #import "BAWKWebView.h" `<br>
* 4、项目源码地址：<br>
 OC 版 ：[https://github.com/BAHome/BAWKWebView](https://github.com/BAHome/BAWKWebView)<br>

## 4、BAWKWebView 的类结构及 demo 示例
![BAWKWebView](https://github.com/BAHome/BAWKWebView/blob/master/Images/BAWKWebView.png)

### BAKit_WebView.h
```
#ifndef BAKit_WebView_h
#define BAKit_WebView_h

#import "WKWebView+Post.h"
#import "BAKit_ConfigurationDefine.h"
#import "WKWebView+BAJavaScriptAlert.h"
#import "WKWebView+BAKit.h"

/*!
 *********************************************************************************
 ************************************ 更新说明 ************************************
 *********************************************************************************
 
 欢迎使用 BAHome 系列开源代码 ！
 如有更多需求，请前往：https://github.com/BAHome
 
 项目源码地址：
 OC 版 ：https://github.com/BAHome/BAWKWebView
 
 最新更新时间：2017-06-15 【倒叙】
 最新Version：【Version：1.0.1】
 更新内容：
 1.0.1.1、适配 iOS 8 和 iOS 9
 
 最新更新时间：2017-06-15 【倒叙】
 最新Version：【Version：1.0.0】
 更新内容：
 1.0.0.1、用分类封装 WKWebView，代码无任何侵入更改
 1.0.0.2、用 block 方式实现所需代理回调，更加方便，代码更简洁
 1.0.0.3、一行代码搞定 request、URL、URLString、本地 HTML文件、HTMLString等请求
 1.0.0.4、两行代码搞定 JS OC互调（目前为止 git 最简便、最快捷有效的 方法）
 1.0.0.5、一个 block 搞定 title、progress、currentURL、当前网页的高度等等所需
 1.0.0.6、有博爱封装好的 BAWebViewController 可以直接使用，也可以参考自定义浏览器【参考demo】
 1.0.0.7、WKWebView 自定义 request post 数据到 JS（使用分类）
 
 */

#endif /* BAKit_WebView_h */
```

### WKWebView+BAKit.h
```
#import <WebKit/WebKit.h>

NS_ASSUME_NONNULL_BEGIN

/**
 开始加载时调用
 
 @param webView webView
 @param navigation navigation
 */
typedef void (^BAKit_webView_didStartProvisionalNavigationBlock)(WKWebView * _Nullable webView, WKNavigation *navigation);

/**
 当内容开始返回时调用
 
 @param webView webView
 @param navigation navigation
 */
typedef void (^BAKit_webView_didCommitNavigationBlock)(WKWebView *webView, WKNavigation *navigation);

/**
 页面加载完成之后调用
 
 @param webView webView
 @param navigation navigation
 */
typedef void (^BAKit_webView_didFinishNavigationBlock)(WKWebView *webView, WKNavigation *navigation);

/**
 页面加载失败时调用
 
 @param webView webView
 @param navigation navigation
 */
typedef void (^BAKit_webView_didFailProvisionalNavigationBlock)(WKWebView *webView, WKNavigation *navigation);

/**
 获取 web 加载进度，判断是否正在加载
 
 @param isLoading 是否正在加载
 @param progress web 加载进度，范围：0.0f ~ 1.0f
 */
typedef void (^BAKit_webView_isLoadingBlock)(BOOL isLoading, CGFloat progress);

/**
 获取 web 的 title
 
 @param title title
 */
typedef void (^BAKit_webView_getTitleBlock)(NSString *title);

/**
 JS 调用 OC 时 webview 会调用此方法
 
 @param userContentController webview中配置的userContentController 信息
 
 @param message JS执行传递的消息
 */
typedef void (^BAKit_webView_userContentControllerDidReceiveScriptMessageBlock)(WKUserContentController *userContentController, WKScriptMessage *message);

typedef void (^BAKit_webView_decidePolicyForNavigationActionBlock)(WKWebView *webView,  WKNavigationAction *navigationAction);

typedef void (^BAKit_webView_getCurrentUrlBlock)(NSURL *currentUrl);


@interface WKWebView (BAKit)
<
    WKNavigationDelegate,
    WKUIDelegate,
    WKScriptMessageHandler
>

/**
 当前网页的高度
 */
@property(nonatomic, assign) CGFloat ba_web_currentHeight;

/**
 是否可以返回上级页面
 */
@property (nonatomic, readonly) BOOL ba_web_canGoBack;

/**
 是否可以进入下级页面
 */
@property (nonatomic, readonly) BOOL ba_web_canGoForward;


@property(nonatomic, copy) BAKit_webView_didStartProvisionalNavigationBlock ba_web_didStartBlock;
@property(nonatomic, copy) BAKit_webView_didCommitNavigationBlock ba_web_didCommitBlock;
@property(nonatomic, copy) BAKit_webView_didFinishNavigationBlock ba_web_didFinishBlock;
@property(nonatomic, copy) BAKit_webView_didFailProvisionalNavigationBlock ba_web_didFailBlock;
@property(nonatomic, copy) BAKit_webView_isLoadingBlock ba_web_isLoadingBlock;
@property(nonatomic, copy) BAKit_webView_getTitleBlock ba_web_getTitleBlock;
@property(nonatomic, copy) BAKit_webView_userContentControllerDidReceiveScriptMessageBlock ba_web_userContentControllerDidReceiveScriptMessageBlock;
@property(nonatomic, copy) BAKit_webView_decidePolicyForNavigationActionBlock ba_web_decidePolicyForNavigationActionBlock;
@property(nonatomic, copy) BAKit_webView_getCurrentUrlBlock ba_web_getCurrentUrlBlock;


#pragma mark - Public method

/**
 添加 WKWebView 的代理，注意：一般不用添加，特殊情况下（代理 block 不走）可以在初始化的时候，用此方法添加代理，例如：        
 BAKit_WeakSelf
 [self.webView ba_web_initWithDelegate:weak_self.webView uIDelegate:weak_self.webView];

 @param navigationDelegate navigationDelegate
 @param uIDelegate uIDelegate
 */
- (void)ba_web_initWithDelegate:(id<WKNavigationDelegate>)navigationDelegate
                     uIDelegate:(id<WKUIDelegate>)uIDelegate;

/**
 *  返回上一级页面
 */
- (void)ba_web_goBack;

/**
 *  进入下一级页面
 */
- (void)ba_web_goForward;

/**
 *  刷新 webView
 */
- (void)ba_web_reload;

/**
 *  加载一个 webview
 *
 *  @param request 请求的 NSURL URLRequest
 */
- (void)ba_web_loadRequest:(NSURLRequest *)request;

/**
 *  加载一个 webview
 *
 *  @param URL 请求的 URL
 */
- (void)ba_web_loadURL:(NSURL *)URL;

/**
 *  加载一个 webview
 *
 *  @param URLString 请求的 URLString
 */
- (void)ba_web_loadURLString:(NSString *)URLString;

/**
 *  加载本地网页
 *
 *  @param htmlName 请求的本地 HTML 文件名
 */
- (void)ba_web_loadHTMLFileName:(NSString *)htmlName;

/**
 *  加载本地 htmlString
 *
 *  @param htmlString 请求的本地 htmlString
 */
- (void)ba_web_loadHTMLString:(NSString *)htmlString;

/**
 *  OC 调用 JS，加载 js 字符串，例如：高度自适应获取代码：
 // webView 高度自适应
 [self ba_web_stringByEvaluateJavaScript:@"document.body.offsetHeight" completionHandler:^(id _Nullable result, NSError * _Nullable error) {
 // 获取页面高度，并重置 webview 的 frame
 self.ba_web_currentHeight = [result doubleValue];
 CGRect frame = webView.frame;
 frame.size.height = self.ba_web_currentHeight;
 webView.frame = frame;
 }];
 *
 *  @param javaScriptString js 字符串
 */
- (void)ba_web_stringByEvaluateJavaScript:(NSString *)javaScriptString completionHandler:(void (^ _Nullable)(_Nullable id result, NSError * _Nullable error))completionHandler;

/**
 JS 调用 OC，addScriptMessageHandler:name:有两个参数，第一个参数是 userContentController的代理对象，第二个参数是 JS 里发送 postMessage 的对象。添加一个脚本消息的处理器,同时需要在 JS 中添加，window.webkit.messageHandlers.<name>.postMessage(<messageBody>)才能起作用。
 
 @param nameArray JS 里发送 postMessage 的对象数组，可同时添加多个对象
 */
- (void)ba_web_addScriptMessageHandlerWithNameArray:(NSArray *)nameArray;


@end
NS_ASSUME_NONNULL_END
```

## BAWebViewController.h
```
NS_ASSUME_NONNULL_BEGIN

@interface BAWebViewController : UIViewController

@property(nonatomic, strong) UIColor * _Nullable ba_web_progressTintColor;
@property(nonatomic, strong) UIColor *ba_web_progressTrackTintColor;

/**
 *  加载一个 webview
 *
 *  @param request 请求的 NSURL URLRequest
 */
- (void)ba_web_loadRequest:(NSURLRequest *)request;

/**
 *  加载一个 webview
 *
 *  @param URL 请求的 URL
 */
- (void)ba_web_loadURL:(NSURL *)URL;

/**
 *  加载一个 webview
 *
 *  @param URLString 请求的 URLString
 */
- (void)ba_web_loadURLString:(NSString *)URLString;

/**
 *  加载本地网页
 *
 *  @param htmlName 请求的本地 HTML 文件名
 */
- (void)ba_web_loadHTMLFileName:(NSString *)htmlName;

/**
 *  加载本地 htmlString
 *
 *  @param htmlString 请求的本地 htmlString
 */
- (void)ba_web_loadHTMLString:(NSString *)htmlString;

/**
 *  加载 js 字符串，例如：高度自适应获取代码：
 // webView 高度自适应
 [self ba_web_stringByEvaluateJavaScript:@"document.body.offsetHeight" completionHandler:^(id _Nullable result, NSError * _Nullable error) {
 // 获取页面高度，并重置 webview 的 frame
 self.ba_web_currentHeight = [result doubleValue];
 CGRect frame = webView.frame;
 frame.size.height = self.ba_web_currentHeight;
 webView.frame = frame;
 }];
 *
 *  @param javaScriptString js 字符串
 */
- (void)ba_web_stringByEvaluateJavaScript:(NSString *)javaScriptString completionHandler:(void (^ _Nullable)(_Nullable id, NSError * _Nullable error))completionHandler;

@end
NS_ASSUME_NONNULL_END
```

### demo 示例
```
// 示例1：
- (void)setupUI
{
    self.view.backgroundColor = BAKit_Color_White;
    self.webView.hidden = NO;
    
    [self configBackItem];
    [self configMenuItem];
    
    
    BAKit_WeakSelf;
    self.webView.ba_web_didStartBlock = ^(WKWebView *webView, WKNavigation *navigation) {
        
        BAKit_StrongSelf
        NSLog(@"开始加载网页");
        // 开始加载网页时展示出progressView
        self.progressView.hidden = NO;
        // 开始加载网页的时候将progressView的Height恢复为1.5倍
        self.progressView.transform = CGAffineTransformMakeScale(1.0f, 1.5f);
        // 防止progressView被网页挡住
        [self.navigationController.view bringSubviewToFront:self.progressView];
        
    };
    
    self.webView.ba_web_didFinishBlock = ^(WKWebView *webView, WKNavigation *navigation) {
        
    };
    
    self.webView.ba_web_isLoadingBlock = ^(BOOL isLoading, CGFloat progress) {
        
        BAKit_StrongSelf
        self.progressView.progress = progress;
        if (self.progressView.progress == 1)
        {
            /*
             *添加一个简单的动画，将progressView的Height变为1.4倍，在开始加载网页的代理中会恢复为1.5倍
             *动画时长0.25s，延时0.3s后开始动画
             *动画结束后将progressView隐藏
             */
            
            [UIView animateWithDuration:0.25f delay:0.3f options:UIViewAnimationOptionCurveEaseOut animations:^{
                self.progressView.transform = CGAffineTransformMakeScale(1.0f, 1.4f);
            } completion:^(BOOL finished) {
                self.progressView.hidden = YES;
                
            }];
        }
        
    };
    
    self.webView.ba_web_getTitleBlock = ^(NSString *title) {
        
        BAKit_StrongSelf
        // 获取当前网页的 title
        self.title = title;
    };
    
    self.webView.ba_web_getCurrentUrlBlock = ^(NSURL * _Nonnull currentUrl) {
        BAKit_StrongSelf
        self.ba_web_currentUrl = currentUrl;
    };
}
    
// 示例2：
    NSString *htmlName = @"BAHome2";
    [self.webView ba_web_loadHTMLFileName:htmlName];

// 示例3：
#pragma mark - JS_OC
- (void)ba_JS_OC
{
    // 1、先注册ID
    NSArray *messageNameArray = @[@"BA_Alert", @"BA_JumpVC", @"BA_SendMsg"];
    [self.webView ba_web_addScriptMessageHandlerWithNameArray:messageNameArray];

    // 2、JS 调用 OC 时 webview 会调用此 block
    BAKit_WeakSelf
    self.webView.ba_web_userContentControllerDidReceiveScriptMessageBlock = ^(WKUserContentController * _Nonnull userContentController, WKScriptMessage * _Nonnull message) {
        BAKit_StrongSelf
        if ([message.name isEqualToString:messageNameArray[0]])
        {
            NSString *msg = @"生命不息，折腾不止...来自 OC Alert！";
            BAKit_ShowAlertWithMsg_ios8(msg);
        }
        else if ([message.name isEqualToString:messageNameArray[1]])
        {
            UIViewController *vc = [UIViewController new];
            vc.view.backgroundColor = BAKit_Color_Green;
            vc.title = @"这里是 JS 按钮跳转的 VC";
            [self.navigationController pushViewController:vc animated:YES];
        }
        else if ([message.name isEqualToString:messageNameArray[2]])
        {
            NSArray *array = message.body;
            NSString *msg = [NSString stringWithFormat:@"这是博爱的手机号: %@, \n%@ !!",array[0], array[1]];
            BAKit_ShowAlertWithMsg_ios8(msg);
        }
    };
}

#pragma mark - OC_JS
- (void)ba_OC_JS
{
    // 3、OC 调用 JS
    NSString *jsMethod = [NSString stringWithFormat:@"ba_insert('18566668888', '生命不息，折腾不止...这里是 OC 插入 JS 的语句！')"];
    [self.webView ba_web_stringByEvaluateJavaScript:jsMethod completionHandler:^(id  _Nullable result, NSError * _Nullable error) {
        
    }];
}

#pragma mark - OC 按钮调用 JS 方法：【JavaScriptCore 库】！
- (IBAction)clickShareBtn:(UIButton *)sender
{
    BAKit_WeakSelf
    if (!self.webView.loading)
    {
        BAKit_StrongSelf
        [self ba_OC_JS];
    }
}

#pragma mark - JS 调用 OC 

- (void)ba_js_OCWithDictionary:(NSDictionary *)dict
{
    if (![dict isKindOfClass:[NSDictionary class]])
    {
        return;
    }
    
    NSString *title = dict[@"title"];
    NSString *content = dict[@"content"];
    NSString *url = dict[@"url"];

    // OC反馈给JS分享结果
    NSString *result = [NSString stringWithFormat:@"ba_shareResult('%@', '%@', '%@')", title, content, url];
    
    // OC 调用 JS
    [self.webView ba_web_stringByEvaluateJavaScript:result completionHandler:^(id  _Nullable result, NSError * _Nullable error) {
        NSLog(@"%@", error);
    }];
}


其他示例可下载demo查看源码！
```

## 5、更新记录：【倒叙】
 欢迎使用 [【BAHome】](https://github.com/BAHome) 系列开源代码 ！
 如有更多需求，请前往：[【https://github.com/BAHome】](https://github.com/BAHome) 
 
 最新更新时间：2017-06-15 【倒叙】
 最新Version：【Version：1.0.1】
 更新内容：
 1.0.1.1、适配 iOS 8 和 iOS 9
 
 最新更新时间：2017-06-15 【倒叙】
 最新Version：【Version：1.0.0】
 更新内容：
 1.0.0.1、用分类封装 WKWebView，代码无任何侵入更改
 1.0.0.2、用 block 方式实现所需代理回调，更加方便，代码更简洁
 1.0.0.3、一行代码搞定 request、URL、URLString、本地 HTML文件、HTMLString等请求
 1.0.0.4、两行代码搞定 JS OC互调（目前为止 git 最简便、最快捷有效的 方法）
 1.0.0.5、一个 block 搞定 title、progress、currentURL、当前网页的高度等等所需
 1.0.0.6、有博爱封装好的 BAWebViewController 可以直接使用，也可以参考自定义浏览器【参考demo】
 1.0.0.7、WKWebView 自定义 request post 数据到 JS（使用分类）
 

## 6、bug 反馈 和 联系方式
> 1、开发中遇到 bug，希望小伙伴儿们能够及时反馈与我们 BAHome 团队，我们必定会认真对待每一个问题！ <br>

> 2、联系方式 <br> 
QQ群：479663605  【注意：此群为 2 元 付费群，介意的小伙伴儿勿扰！】<br> 
博爱QQ：137361770 <br> 
博爱微博：[![](https://img.shields.io/badge/微博-博爱1616-red.svg)](http://weibo.com/538298123) <br> 

## 7、开发环境 和 支持版本
> 开发使用 Xcode Version 8.3.2 (8E2002) ，理论上支持所有 iOS 版本，如有版本适配问题，请及时反馈！多谢合作！

## 8、感谢
> 感谢 BAHome 团队成员倾力合作，后期会推出一系列 常用 UI 控件的封装，大家有需求得也可以在 issue 提出，如果合理，我们会尽快推出新版本！<br>

> BAHome 的发展离不开小伙伴儿的信任与推广，再次感谢各位小伙伴儿的支持！

