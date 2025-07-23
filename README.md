# Chinese Mini-app and Mini-game Market Adaptation (Knowhows I learned)

This repository is a personal collection of notes, insights, and lessons I've picked up while adapting mini-apps and mini-games for the Chinese market — especially for platforms like WeChat (微信) and Douyin (抖音, TikTok China).
It's not a comprehensive guide or a universal blueprint, but rather a set of practical takeaways based on real-world experience. I hope that by sharing what I've learned, others exploring the same path might find something useful or avoid a few common pitfalls.


## 微信(Wechat)

WeChat offers a unique feature that lets developers build lightweight applications — known as mini-apps and mini-games — that run inside the WeChat app itself. Over the years, this feature has evolved into a massive ecosystem, giving users access to games, services, and utilities without ever needing to install a separate app.

The runtime of the miniapps and minigames are modified version of the web browser - almost compatible with HTML5, Javascript, and other browser-based technologies including WebGL with some exceptions and custom APIS.

### 小游戏(Mini-games)

[Developer Guide](https://developers.weixin.qq.com/minigame/dev/guide/)

As there are many different libraries that are used to develop HTML5/WebGL/Javascript games.
Therefore there isn't a single fully-proven way of converting any browser games into minigames.
The most viable way for conversion would be using *Adapter*.

[Adaptor Tutorial](https://developers.weixin.qq.com/minigame/en/dev/tutorial/base/adapter.html)

#### HTML5 game to minigame

There are bunch of adapters out there. (You will see if you look up by "weapp-adapter" on Github)

The most basic one would be `weapp-adapter`, official base for writing adapters for wechat minigames.

It is hosted on Github at the following address:
[Weapp Adapter](https://github.com/finscn/weapp-adapter)

#### Unity game to Wechat minigame

Unity has been pushing its position in Chinese market by strengthening relationships with their Chinese partners.

For smaller Unity games, the conversion to wechat minigame was doable using the following plugin.
Previously a community project, it seems to be supported by Wechat officially (almost).

[Unity-to-minigame conversion guideline](https://wechat-miniprogram.github.io/minigame-unity-webgl-transform/)
[Unity-to-minigame conversion plugin](https://github.com/wechat-miniprogram/minigame-tuanjie-transform-sdk)

## 抖音(TikTok).

Compared to Wechat, TikTok mini-app and mini-game ecosystem is still maturing.
One of the biggest drawback is that their SDKs are still closed-sourced, and community projects are not found.

### 小游戏(Mini-games)

### Unity game to Tiktok minigame




