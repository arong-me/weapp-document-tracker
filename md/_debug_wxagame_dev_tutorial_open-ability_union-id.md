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

*   [中文](https://developers.weixin.qq.com/minigame/dev/tutorial/open-ability/union-id.html?t=18091022)<span class="split-line">/</span>
*   [EN](https://developers.weixin.qq.com/minigame/en/dev/tutorial/open-ability/union-id.html?t=18091022)

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

*   [中文](https://developers.weixin.qq.com/minigame/dev/tutorial/open-ability/union-id.html?t=18091022)<span class="split-line">/</span>
*   [EN](https://developers.weixin.qq.com/minigame/en/dev/tutorial/open-ability/union-id.html?t=18091022)

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
*   [可用性](../usability/debug.html)
    *   [调试](../usability/debug.html)
    *   [性能](../usability/performance.html)
    *   [小游戏更新](../usability/update.html)
    *   [多线程 Worker](../usability/worker.html)
*   [开放能力](./authorize.html)
    *   [用户授权](./authorize.html)
    *   [游戏圈使用指南](./game-club.html)
    *   [用户登录态签名](./http-signature.html)
    *   [米大师支付签名](./midas-signature.html)
    *   [关系链数据使用指南](./open-data.html)
    *   [虚拟支付](./payment.html)
    *   [获取二维码](./qrcode.html)
    *   [排行榜配置指引](./ranklist.html)
    *   [转发](./share.html)
    *   [用户数据的签名验证和加解密](./signature.html)
    *   [UnionID 机制说明](./union-id.html)
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

## UnionID 机制说明

如果开发者拥有多个移动应用、网站应用、和公众帐号（包括小游戏），可通过unionid来区分用户的唯一性，因为只要是同一个微信开放平台帐号下的移动应用、网站应用和公众帐号（包括小游戏），用户的unionid是唯一的。换句话说，同一用户，对同一个微信开放平台下的不同应用，unionid是相同的。

### UnionID获取途径

绑定了开发者帐号的小游戏，可以通过下面3种途径获取UnionID。

1.  调用接口[wx.getUserInfo](../../api/open-api/user-info/wx.getUserInfo.html)，从解密数据中获取 UnionID。注意本接口需要用户授权，请开发者妥善处理用户拒绝授权后的情况。

2.  如果开发者帐号下存在**同主体的**公众号，并且该用户已经关注了该公众号。开发者可以直接通过[wx.login](../../api/open-api/login/wx.login.html)获取到该用户UnionID，无须用户再次授权。

3.  如果开发者帐号下存在**同主体的**公众号或移动应用，并且该用户已经授权登录过该公众号或移动应用。开发者也可以直接通过[wx.login](../../api/open-api/login/wx.login.html)获取到该用户UnionID，无须用户再次授权。

### 微信开放平台绑定小游戏流程

前提：微信开放平台帐号必须已完成开发者资质认证

开发者资质认证流程：

登录微信开放平台(open.weixin.qq.com) – 帐号中心 – 开发者资质认证

![img](https://developers.weixin.qq.com/minigame/dev/tutorial/image/open.png?t=18091022)

绑定流程：

登录微信开放平台（open.weixin.qq.com）—管理中心—公众帐号—绑定公众帐号

![img](https://developers.weixin.qq.com/minigame/dev/tutorial/image/union_bind.png?t=18091022)

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

[](./signature.html)</div>

</div>