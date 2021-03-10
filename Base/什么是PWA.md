# PWA

## 背景

大家都知道Native app体验确实很好，下载到手机上之后入口也方便。  
它也有一些缺点：  
- 开发成本高(ios和安卓)
- 软件上线需要审核
- 版本更新需要将新版本上传到不同的应用商店
- 想使用一个app就必须去下载才能使用，即使是偶尔需要使用一下下

而web网页开发成本低，网站更新时上传最新的资源到服务器即可，用手机带的浏览器打开就可以使用，但是还有一些明显的缺点。  
web网页缺点：  
- 体验上比Native app差
- 手机桌面入口不够便捷，想要进入一个页面必须要记住它的url或者加入书签
- 没网络就没响应，不具备离线能力
- 不像APP一样能进行消息推送


## PWA

`PWA（Progressive Web App，即渐进式WEB应用）`是一种理念，使用多种技术来增强web app的功能，可以让网站的体验变得更好，能够模拟一些Native app功能，比如通知推送等。在移动端利用标准化框架，让网页应用呈现和Native app相似的体验。  

> 官网 https://web.dev/progressive-web-apps/  
> 更多参考 https://developer.mozilla.org/zh-CN/docs/Web/Progressive_web_apps  

一个 PWA 应用首先是一个网页程序, 可以通过 Web 技术编写出一个网页应用. 随后添加上 App Manifest 和 Service Worker 来实现 PWA 的安装和离线等功能
解决了哪些问题？  

- 可以添加至主屏幕，点击主屏幕图标可以实现启动动画以及隐藏地址栏
- 实现离线缓存功能，即使用户手机没有网络，依然可以使用一些离线功能
- 实现了消息推送

它解决了上述提到的问题，这些特性将使得 Web 应用渐进式接近原生 App。

## PWA的实现

PWA关键结构

1. Manifest （应用清单）
2. Service Worker （可以理解为服务工厂）
3. Push Notification（推送通知）

### Manifest
Web App Manifest 是一个 W3C 规范，它定义了一个基于 JSON 的 List 。Manifest 在 PWA 中的作用有：

​ 能够将你浏览的网页添加到你的手机屏幕上

​ 在 Android 上能够全屏启动，不显示地址栏 （ 由于 Iphone 手机的浏览器是 Safari ，所以不支持哦）

​ 控制屏幕 横屏 / 竖屏 展示

​ 定义启动画面

​ 可以设置你的应用启动是从主屏幕启动还是从 URL 启动

​ 可以设置你添加屏幕上的应用程序图标、名字、图标大小

示例：  
// index.html
```
<head>
  <title>Minimal PWA</title>
  <meta name="viewport" content="width=device-width, user-scalable=no" />
  <link rel="manifest" href="manifest.json" />
  <link rel="stylesheet" type="text/css" href="main.css">
  <link rel="icon" href="/e.png" type="image/png" />
</head>
```
// manifest.json
```
{
  "name": "Minimal PWA", // 必填 显示的插件名称
  "short_name": "PWA Demo", // 可选  在APP launcher和新的tab页显示，如果没有设置，则使用name
  "description": "The app that helps you understand PWA", //用于描述应用
  "display": "standalone", // 定义开发人员对Web应用程序的首选显示模式。standalone模式会有单独的
  "start_url": "/", // 应用启动时的url
  "theme_color": "#313131", // 桌面图标的背景色
  "background_color": "#313131", // 为web应用程序预定义的背景颜色。在启动web应用程序和加载应用程序的内容之间创建了一个平滑的过渡。
  "icons": [ // 桌面图标，是一个数组
    {
    "src": "icon/lowres.webp",
    "sizes": "48x48",  // 以空格分隔的图片尺寸
    "type": "image/webp"  // 帮助userAgent快速排除不支持的类型
  },
  {
    "src": "icon/lowres",
    "sizes": "48x48"
  },
  {
    "src": "icon/hd_hi.ico",
    "sizes": "72x72 96x96 128x128 256x256"
  },
  {
    "src": "icon/hd_hi.svg",
    "sizes": "72x72"
  }
  ]
}
```
> Manifest参考文档：https://developer.mozilla.org/zh-CN/docs/Web/Manifest
