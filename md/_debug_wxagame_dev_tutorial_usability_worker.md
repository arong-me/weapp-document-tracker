<div class="book with-summary">

<div class="head">

<div class="head_box">

# [](javascript:; "_('微信公众平台 小程序')")

<div class="header_ctrls">

*   [介绍](javascript:;)
    *   [小程序介绍](https://developers.weixin.qq.com/miniprogram/introduction/index.html?t=18091022)
    *   [小游戏介绍](https://developers.weixin.qq.com/minigame/introduction/index.html?t=18091022)
*   [设计](https://developers.weixin.qq.com/miniprogram/design/index.html?t=18091022)
*   [小游戏开发](javascript:;)
    *   [小程序开发](https://developers.weixin.qq.com/miniprogram/dev/index.html?t=18091022)
    *   [小游戏开发](https://developers.weixin.qq.com/minigame/dev/index.html?t=18091022)
*   [运营](https://developers.weixin.qq.com/miniprogram/product/index.html?t=18091022)
*   [数据](javascript:;)
    *   [小程序数据](https://developers.weixin.qq.com/miniprogram/analysis/index.html?t=18091022)
    *   [小游戏数据](https://developers.weixin.qq.com/minigame/analysis/index.html?t=18091022)
*   [社区](https://developers.weixin.qq.com/)

*   [中文](https://developers.weixin.qq.com/minigame/dev/tutorial/usability/worker.html?t=18091022)<span class="split-line">/</span>
*   [EN](https://developers.weixin.qq.com/minigame/en/dev/tutorial/usability/worker.html?t=18091022)

</div>

</div>

</div>

<div class="sub_nav_box">

<div class="sub_nav_inner">

<div class="book-summary-opr" id="js-book-summary-opr"><a class="book-summary-btn"></a></div>

<div class="top_sub_nav">

<div class="top_title_wap"><span class="icon_title icon_dev"></span>

微信小游戏开发文档

</div>

*   [教程](../../)
*   [API](../../api/render/canvas/wx.createCanvas.html)
*   [工具](../../devtools/devtools.html)
*   [小程序·云开发](../../wxcloud/basis/getting-started.html)

</div>

<div id="book-search-input" role="search">

<form><label for="search-input" class="search-icon" id="js-search-icon"></label><input type="text" id="search-input" name="search-input" placeholder="搜索"> </form>

</div>

*   [中文](https://developers.weixin.qq.com/minigame/dev/tutorial/usability/worker.html?t=18091022)<span class="split-line">/</span>
*   [EN](https://developers.weixin.qq.com/minigame/en/dev/tutorial/usability/worker.html?t=18091022)

</div>

</div>

<div class="book-summary">

<div class="book-summary-home" id="js-summary-home"><a><span class="icon_home_s icon_dev"></span><span class="s_title_2">开发文档首页</span></a></div>

<nav role="navigation">

*   [基础](../../)
    *   [快速上手](../../)
    *   [Adapter](../base/adapter.html)
    *   [对引擎的支持](../base/engine.html)
    *   [模块化](../base/module.html)
    *   [分包加载](../base/subpackages.html)
*   [能力](../ability/audio.html)
    *   [音频播放](../ability/audio.html)
    *   [文件系统](../ability/file-system.html)
*   [可用性](./debug.html)
    *   [调试](./debug.html)
    *   [性能](./performance.html)
    *   [小游戏更新](./update.html)
    *   [多线程 Worker](./worker.html)
*   [开放能力](../open-ability/authorize.html)
    *   [用户授权](../open-ability/authorize.html)
    *   [游戏圈使用指南](../open-ability/game-club.html)
    *   [用户登录态签名](../open-ability/http-signature.html)
    *   [米大师支付签名](../open-ability/midas-signature.html)
    *   [关系链数据使用指南](../open-ability/open-data.html)
    *   [虚拟支付](../open-ability/payment.html)
    *   [获取二维码](../open-ability/qrcode.html)
    *   [排行榜配置指引](../open-ability/ranklist.html)
    *   [转发](../open-ability/share.html)
    *   [用户数据的签名验证和加解密](../open-ability/signature.html)
    *   [UnionID 机制说明](../open-ability/union-id.html)
*   [广告](../ad/banner-ad.html)
    *   [Banner 广告](../ad/banner-ad.html)
    *   [激励视频广告](../ad/rewarded-video-ad.html)

</nav>

</div>

<div class="book-body">

<div class="body-inner">

<div class="page-wrapper" tabindex="-1" role="main">

<div class="page-inner">

<div id="book-search-results">

<div class="search-noresults">

<section class="normal markdown-section">

## 多线程 Worker

对于游戏来说，每帧 16ms 是极其宝贵的，如果有一些可以异步处理的任务，可以放置于 [Worker](../../api/worker/Worker.html) 中运行，待运行结束后，再把结果返回到主线程。[Worker](../../api/worker/Worker.html) 运行于一个单独的全局上下文与线程中，不能直接调用主线程的方法，[Worker](../../api/worker/Worker.html) 也不具备渲染的能力。 [Worker](../../api/worker/Worker.html) 与主线程之间的数据传输，双方使用 [Worker.postMessage()](../../api/worker/Worker.postMessage.html) 来发送数据，[Worker.onMessage()](../../api/worker/Worker.onMessage.html) 来接收数据，传输的数据并不是直接共享，而是被复制的。

#### 步骤

##### 1\. 配置 Worker 信息

在 `game.json` 中可配置 `Worker` 代码放置的目录，目录下的代码将被打包成一个文件：

配置示例：

    {
      "workers": "workers"
    }

##### 2\. 添加 Worker 代码文件

根据步骤 1 中的配置，在代码目录下新建以下两个入口文件：

    workers/request/index.js
    workers/request/utils.js
    workers/response/index.js

添加后，目录结构如下：

    ├── game.js
    ├── game.json
    ├── project.config.json
    └── workers
        ├── request
        │   ├── index.js
        │   └── utils.js
        └── response
            └── index.js

#### 3\. 编写 Worker 代码

在 `workers/request/index.js` 编写 Worker 响应代码

    var utils = require('./utils')

    // 在 Worker 线程执行上下文会全局暴露一个 `worker` 对象，直接调用 worker.onMeesage/postMessage 即可
    worker.onMessage(function (res) {
      console.log(res)
    })

#### 4\. 在主线程中初始化 Worker

在主线程的代码 game.js 中初始化 Worker

    var worker = wx.createWorker('workers/request/index.js') // 文件名指定 worker 的入口文件路径，绝对路径

#### 5\. 主线程向 Worker 发送消息

    worker.postMessage({
      msg: 'hello worker'
    })

worker 对象的其它接口请看 [worker接口说明](../../api/worker/Worker.html)

#### Tips

1.  Worker 最大并发数量限制为 1 个，创建下一个前请用 [Worker.terminate()](../../api/worker/Worker.terminate.html) 结束当前 Worker
2.  Worker 内代码只能 require 指定 Worker 路径内的文件，无法引用其它路径
3.  Worker 的入口文件由 [wx.createWorker()](../../api/worker/wx.createWorker.html) 时指定，开发者可动态指定 Worker 入口文件
4.  Worker 内不支持 `wx` 系列的 API
5.  Workers 之间不支持发送消息

</section>

</div>

<div class="search-results">

<div class="has-results">

# <span class="search-results-count"></span>个结果 "<span class="search-query"></span>"

</div>

<div class="no-results">

# 没有找到相关内容 "<span class="search-query"></span>"

</div>

</div>

</div>

</div>

</div>

<div class="foot" id="footer">

*   [关于腾讯](https://www.tencent.com/)
*   [文档中心](https://developers.weixin.qq.com/miniprogram/introduction/index.html)
*   [辟谣中心](https://mp.weixin.qq.com/cgi-bin/opshowpage?action=dispelinfo)
*   [客服中心](https://kf.qq.com/product/wx_xcx.html)
*   [联系邮箱](mailto:weixinmp@qq.com)
*   Copyright © 2012-<span id="s_copyright_year"></span> Tencent. All Rights Reserved.

</div>

</div>

[](./update.html)</div>

</div>