## Performance 工具篇
Chrome DevTools 自带的 performance 工具，可以帮助我们分析网页的性能问题，从而帮助我们优化网页的性能。

### 马上试试
1. 首先要打开无痕窗口，这样最大程度可以避免其他插件的干扰。
1. 打开 Chrome DevTools，点击 Performance 面板。
1. 点击 Record 按钮，开始录制，需要主动 stop 进行关闭。reload 按钮则会刷新页面并录制，会自动关闭，适合记录首屏渲染。
1. 在录制的过程中，你可以在页面上进行操作，比如点击按钮、滚动页面等。


### Chrome Performance 工具使用

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1e7f35af98f345adb83d003de70af6bf~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

Chrome 中Performance可以在上图中看到，主要分了几个板块

### 控制面板（Controls）

开启记录，停止记录，配置记录期间需要记录的内容。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f3a9439d58d34d698ed08354a44eadd8~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

操作主要分了2个区域，操作1区从左到右依次是 "Record/Stop"、"Reload"和"Clear"，

-   "Record/Stop"：一般用于录制页面交互过程的性能变化数据，选择任意想要测试的过程，点击"Record"，并在测量结束之后，点击"Stop"，之后Chrome就会自动解析这段时间内抓取的数据，并生成报告。
-   "Reload"：一般用于录制首屏加载的性能变化数据，它会自动刷新整个页面，并开始记录性能。
-   "Clear"：用于清除性能报告数据

操作2区可以选择报告展示内容，从左到右依次是 Screenshots、Memory、Web Vitals

-   Screenshots：打开后可以在概览区看到屏幕的截图
-   Memory：打开内存监控
-   WebVitals

### 概览面板（Overview）

主要是对页面表现行为的一个概述，区域由三个图形记录组成。

-   FPS（Frames Per Second）:绿色的柱越高， FPS 值也越高。FPS 图表上方的红色小块指明了长帧(long frame)，这些可能是卡顿。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/04e8073eceab4330a5f6de06ddbb27e2~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

-   CPU(CPU Resources):这个面积图(area chart)表明了哪种事件在消耗 CPU 资源。

-   NET:每种不同颜色的条代表一种资源。
    
    -   条越长表明获取该资源所花的时间越长。

-   每个条中的浅色部分代表等待时间（资源请求被发送到收到第一个响应字节的时间），深色部分代表文件传输时间（从收到第一个字节到这个资源完全被下载好）
    
-   蓝色 代表 HTML 文件，黄色 代表 Script 文件，紫色 代表 Stylesheets 文件， 绿色 代表 Media 文件，灰色 代表其他资源。
    

### 火焰图（Flame Chart）

-   火焰图（Flame Chart）: 可视化 CPU 堆栈(stack)信息记录。
    
    -   从不同的角度分析框选区域 。例如：Network，Frames, Interactions, Main等
        
    -   在火焰图面板上你可能看到三根垂直的线，蓝线代表 DOMContentLoaded 事件，绿线代表渲染开始的时间( time to first paint)，红线代表 load 事件。
        

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7257321387ee4532b71161de2b6d2063~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

其实这里我们主要需要关注Main，因为他是主线程的一个执行情况的监控。点开后，我们可以看当前线程里面一些任务的执行堆栈耗时，我们需要重点关注一些标红（也就是有较高耗时）的任务。

### 详细信息（Detail）

当有具体事件被选择时，该面板展示这个事件的更多详细信息。如果没有事件被选择，该面板展示当前所选时间段的一些信息。详细面板支持精确到毫秒级别的分析，详细面板主要分了

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9c42c43029e241f881f5c240b1137323~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

-   Summary面板：从宏观层面概括了浏览器加载的总时间，主要记录了各个阶段的名称、占用时间、颜色信息。 这里一般来说，需要着重关注的有两个：一是黄色的区域，代表脚本执行时间，另一个是紫色的渲染时间。这两个时间的耗时，是影响页面性能的主要因素。    
    -  Loading: 加载
        
    -  Scripting: 脚本
        
    -  Rendering: 渲染
        
    -  Painting: 绘制
        
    -  Other: 其他
        
    -  Idle: 空闲
        

-   Bottom-Up面板：Bottom-Up中一共三列数据
    
    -   Self Time：代表任务自身执行所消耗的时间。
    -   Total Time：代表此任务及其调用的附属子任务一共消耗的时间。
    -   Activity：具体的活动，部分带有Source Map链接，可以直接定位到花费时间的具体源码，方便我们进行定位和优化。Activity中也有标注各自的颜色，和Summary中颜色是对应的。可以根据颜色快速判断是脚本执行、加载、还是渲染过程。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/faa82400a3554f0993091ed77ffcc83b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

-   Call-Tree面板：Bottom-Up类似事件冒泡，Call Tree类似事件捕获。自上而下的Call-Tree更符合我们的人类正常思维，可以更直观地分析浏览器对页面的build精确到毫秒级的情况
-   Event-Log面板：展示所有阶段包括loading、javascripting、rendering、painting中各事件的耗时情况，并提供了filter输入框和按钮供你快速过滤，常见的优化级别中一般用不到它。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ddede8c3b097447bb89fa31bdd4a5598~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

## Performance Api 监测网页性能

各个浏览器厂商基于标准提供了基础Api，这些Api可以提供检测白屏时间、首屏时间、用户可操作的时间节点，页面总下载的时间、DNS查询的时间、TCP链接的时间等。我们可利用这个搭建一个性能监控工具，监控系统包含了数据采集->数据存储->清洗->监控几个过程，在这里的 demo 就只考虑采集阶段。

### 提供的能力

1.  属性篇

performance的所有Api&property挂载在window下面的performance属性中，可以看到目前提供的一系列属性，关于各个属性的介绍，参照网上对aip的解释，有大量资料可供查询。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cb6029a7ab6d45c18a9b7b86f876029f~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

如上图所展现，performance包含三个对象，分别为 **memory、navigation、timing**

-   memory：是和内存相关的，其提供对内存使用情况的描述，我们可以使用这个属性来订阅页面内存变化情况
    
    -   jsHeapSizeLimit：堆内存大小的限制
    -   totalJSHeapSize：总堆内存的大小
    -   usedJSHeapSize：已经使用的堆内存大小
-   navigation：含义是页面的来源信息，表述页面怎么跳转过来的，该对象有2个属性值
    
    -   redirectCount **：** 记录重定向次数，如果有重定向的话，页面通过几次重定向跳转而来，默认为0
    -   type **：** 页面打开的方式，默认为0，可取值为「0：表示正常进入该页面(非刷新、非重定向)」、「1：表示通过 window.location.reload 刷新的页面」、「2：表示通过浏览器的前进、后退按钮进入的页面」、「255：表示非以上的方式进入页面的」
-   timing：提供页面加载过程中一系列关键时间点的高精度测量，它包含了网络、解析、加载等一系列的时间数据，我们监控网页性能也是基于此提供的属性。为了方便理解，从网上找了一张图片来解释关键节点的含义。
    

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4795c1016e594c2ab81750f32a97cf23~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

-   navigationStart **：** 一个页面卸载结束时的时间戳。如果没有上一个页面的话，那么该值会和fetchStart的值相同
-   redirectStart **:** 第一个http重定向开始的时间戳，如果没有重定向，或者重定向到一个不同源的话，那么该值返回为0
-   redirectEnd **:** 最后一个HTTP重定向完成时的时间戳。如果没有重定向，或者重定向到一个不同的源，该值也返回为0
-   fetchStart **:** 浏览器准备好使用http请求抓取文档的时间(发生在检查本地缓存之前)。
-   domainLookupStart **:** DNS域名查询开始的时间，如果使用了本地缓存话，或持久链接，该值则与fetchStart值相同
-   domainLookupEnd **:** DNS域名查询完成的时间，如果使用了本地缓存话，或 持久链接，该值则与fetchStart值相同
-   connectStart **:** HTTP 开始建立连接的时间，如果是持久链接的话，该值则和fetchStart值相同，如果在传输层发生了错误且需要重新建立连接的话，那么在这里显示的是新建立的链接开始时间
-   secureConnectionStart **:** HTTPS 连接开始的时间，如果不是安全连接，则值为 0
-   connectEnd：HTTP完成建立连接的时间(完成握手)。如果是持久链接的话，该值则和fetchStart值相同，如果在传输层发生了错误且需要重新建立连接的话，那么在这里显示的是新建立的链接完成时间
-   requestStart **:** http请求读取真实文档开始的时间，包括从本地读取缓存，链接错误重连时
-   responseStart **:** 开始接收到响应的时间(获取到第一个字节的那个时候)。包括从本地读取缓存
-   responseEnd **：** HTTP响应全部接收完成时的时间(获取到最后一个字节)。包括从本地读取缓存
-   unloadEventStart **:** 前一个网页（和当前页面同域）unload的时间戳，如果没有前一个网页或前一个网页是不同的域的话，那么该值为0
-   unloadEventEnd **:** 和 unloadEventStart 相对应，返回是前一个网页unload事件绑定的回调函数执行完毕的时间戳。
-   domLoading **:** 开始解析渲染DOM树的时间
-   domInteractive **:** 完成解析DOM树的时间（只是DOM树解析完成，但是并没有开始加载网页的资源）
-   domContentLoadedEventStart **：** DOM解析完成后，网页内资源加载开始的时间
-   domContentLoadedEventEnd **:** DOM解析完成后，网页内资源加载完成的时间
-   domComplete **:** DOM树解析完成，且资源也准备就绪的时间。Document.readyState 变为 complete，并将抛出 readystatechange 相关事件
-   loadEventStart **:** load事件发送给文档。也即load回调函数开始执行的时间，如果没有绑定load事件，则该值为0
-   loadEventEnd **:** load事件的回调函数执行完毕的时间，如果没有绑定load事件，该值为0

2.  方法篇

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f740fe7ef96a46c593017a053172c026~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

如上图，截取的图片，Performance提供了一些，这里我主要介绍一下now()方法和getEntries()方法。其他的网上资料也比较多和全，可以查阅 [juejin.cn/post/684490…](https://juejin.cn/post/6844903801518981133#heading-54 "https://juejin.cn/post/6844903801518981133#heading-54")

-   now方法：提供精度相对较高的时间计算主要有下面两个特点
    
    -   和JavaScript中其他可用的时间类函数（比如`Date.now`）不同的是，`window.performance.now()`返回的时间戳没有被限制在一毫秒的精确度内，相反，它们以浮点数的形式表示时间，精度最高可达微秒级。
    -   另外一个不同点是，`window.performance.now()`是以一个恒定的速率慢慢增加的，它不会受到系统时间的影响（系统时钟可能会被手动调整或被NTP等软件篡改）。

我们可以用这个方法来衡量函数执行的时间，达到监控函数执行效率的效果

```
const fun = () => {

    // do something

}

const startExcuteTime = window.performance.now();

fun();

const endExcuteTime = window.performance.now();

console.log("fun函数执行了" + (endExcuteTime - startExcuteTime) + "毫秒.")

```

-   getEntries方法：通过该方法，我们能够拿到页面所有资源请求的详细情况，这个方法返回值根据传入的参数不同会有不同。但返回值的结构都是一样的，都是一个对象数组，每个对象是对资源的请求过程的描述，在console调用 performance.getEntries()，可以直接看到当前页面所有资源的加载过程。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3a71f44d40774e349abdb8d95457f8a8~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

点开数组中的元素，每个元素详细记录了资源请求关键节点的时间，所以我们完全可以利用这个来实现对资源的请求监控。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/497db3d975b9420da4b3a745962692d5~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

更多Api细节，可以参考司内文章 [再看一次 Performance 接口](https://bytedance.feishu.cn/docs/doccnZoHj24ab8HVh42aQEowZGh# "https://bytedance.feishu.cn/docs/doccnZoHj24ab8HVh42aQEowZGh#")

### 简单实现指标计算

一个监控系统大致可以分为这个下面阶段，我们这里就先关注一下数据的采集阶段。数据采集阶段设计到两点，一个是数据的搜集，一个是数据的上报。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f54dad662dfd4f0a966c57d0adcd3c9e~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

-   数据的搜集：数据搜集依赖于Performance Api拿到性能数据，我们参照一定的计算指标，得到计算值的集合。
-   数据的上报：将搜集到的数据上报到服务器，上报使用的方式也就是发送一个http请求， 不过目前因为监控数据采用XHR的请求上报，受到条件限制比较多，数据容易丢失，容易漏报，且对页面性能有一定的影响。而sendBecan是浏览器为了解决这些问题，它会使用户代理在有机会时异步地向服务器发送数据，同时不会延迟页面的卸载或影响下一导航的载入性能。这就解决了提交分析数据时的所有的问题：数据可靠，传输异步并且不会影响下一页面的加载。具体可以参考：[developer.mozilla.org/zh-CN/docs/…](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FAPI%2FNavigator%2FsendBeacon "https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon")

下面是Slardar源码截图，可以看到他们上报监控数据优先采用的sendBecan，降级策略为XHR请求。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e5b5f96f72ef4f038f8efbd6cbb3222c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

可以通过performance api来实现我们经常关注的一些指标的计算和上报

```
重定向耗时 = redirectEnd - redirectStart;

DNS查询耗时 = domainLookupEnd - domainLookupStart;

TCP链接耗时 = connectEnd - connectStart;

HTTP请求耗时 = responseEnd - responseStart;

解析dom树耗时 = domComplete - domInteractive;

白屏时间 = responseStart - navigationStart; 

DOMready时间 = domContentLoadedEventEnd - navigationStart;

onload时间 = loadEventEnd - navigationStart;
```


## 参考文档

[深入浅出 Performance 工具 & API](https://juejin.cn/post/7000728875676205086)