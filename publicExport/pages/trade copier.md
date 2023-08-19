---
title: trade copier
tags:
categories:
date: 2023-07-29
lastMod: 2023-07-29
---
[[type]]: [[BPA]]
deadline: [[Sep 22nd, 2023]]



## Goals

  + 提前测试两个账户同时操作的copier

  + 免费方案

## steps

  + https://www.fxblue.com/appstore/62/mt5-personal-trade-copier

  + 找到的网站

  + 目前安装有报错

  + YouTube有相关视频

  + 还没做深入调查

    + 试了好几种方案，还花钱是了google voice 也不行，37一个短信，贵死

    + 发现一个可以免费发短信的网站 http://www.textem.net/index.php

  + {{video https://www.youtube.com/watch?v=JZZ-kZCkfkU}}

    + @00:01:32 原来要安装两个mt5软件 打开，然后不是在一个软件上面

    + @00:06:46 视频里的订单也是，成功下单后才会复制过去，limit order 不行

    + 

    + 配置好软件后发现报错 10026 10027

![image.png](/assets/image_1690477341279_0.png)

      + https://www.mql5.com/en/docs/constants/errorswarnings/enum_trade_return_codes 报错代码

      + 似乎TFT 限制了Algo功能，看来只能手搓了

      + https://www.fxblue.com/appstore/u62/mt5-personal-trade-copier/user-guide#toc3.5

        + Fx blue 的说明书真的非常详细

  + **新线索**

    + {{< logseq/orgQUOTE >}}Automated trading disabled (MT4 error #4112, MT5 error #10026): usually means that your account has multiple versions of each symbol, such as EURUSD and EURUSD+, and you are trying to trade the wrong one. Automated trading is not usually disabled; more commonly means that the symbol version you are trying to trade is disabled by the broker and only included in the account for internal purposes. You typically need to use the ForexSymbolSuffix setting or a CustomSymbolMapping to tell the copier to trade a different version of the symbol.
{{< / logseq/orgQUOTE >}}

      + 这个错误一般意味着您的账户有多个版本的每个交易品种，如EURUSD和EURUSD+，而您正在尝试交易错误的版本。自动交易通常不会被禁用；更常见的情况是您要交易的交易品种版本被经纪人禁用，只在账户内部使用。您通常需要使用ForexSymbolSuffix设置或CustomSymbolMapping来告诉复制程序交易该交易品种的不同版本。

    + {{< logseq/mark >}}看来还有研究的可能性{{< / logseq/mark >}}

      + 问题是， 我已经试过了XAUUSDx 的方案，想不到其他的了？

      + IncludeSymbols Sender账户的这个参数，设置了之后就没有报错，但是订单还是发不过去

      + ~~现在我的测试方式是，market order， 使用limit order 没有任何反应~~ 已搞清楚

![image.png](/assets/image_1690479470126_0.png)

        + suffix 功能就说 前后缀设置， 比如cx，x这种

        + Mapping 则是更加精确的对应

```apl
# 报错日志，暂时处理到这里 July 28 02:00
ML	0	00:55:46.067	Experts	automated trading is disabled
LG	2	01:29:08.243	Trades	'347913': failed market buy 0.04 XAUUSDx [AutoTrading disabled by server]
EP	0	01:31:17.958	Experts	automated trading is disabled
LF	0	01:31:25.432	Experts	automated trading is enabled
  EP	2	01:39:21.882	Trades	'347913': failed market buy 0.04 XAUUSDx [AutoTrading disabled by server]
NN	2	01:40:34.306	Trades	'347913': failed market buy 0.04 AUDUSDx [AutoTrading disabled by server]
OJ	2	01:41:23.490	Trades	'347913': failed market buy 0.04 AUDUSDx [AutoTrading disabled by server]
FG	2	01:43:16.358	Trades	'347913': failed market buy 0.04 AUDUSDx [AutoTrading disabled by server]
DS	2	01:45:46.052	Trades	'347913': failed market buy 0.04 AUDUSDx [AutoTrading disabled by server]
```

      + ### 相关帖子

        + https://mqldiscussions.com/t/auto-trading-disabled-from-server-broker/817/2

        + https://www.mql5.com/en/forum/212168 一篇帖子谈到类似情况，似乎无法解决

        + https://www.mql5.com/en/forum/364455/page2

        + https://www.trade-copier.com/index.php/component/cockpit/?view=v4&layout=tutorials_account_settings 这个网站有免费试用copier

        + https://www.mql5.com/en/forum/15410 这篇有讲最后联系broker 开启了功能

## Definition of Done


