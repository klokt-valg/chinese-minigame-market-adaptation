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


#### When running converted app on Tiktok Developer Tool, I see an error like `s.doAccess() does not exist`.

Here's the error message:
```
uncaught (in promise) TypeError: s.doAccess is not a function
    at ___syscall_faccessat (abfs-syscalls.ts:95)
    at access (wasm://wasm/09f1a45a:wasm-function[1046]:0x71615)
    at il2cpp::os::PathErrnoToErrorCode(std::__2::basic_string<char, std::__2::char_traits<char>, std::__2::allocator<char>> const&, int) (wasm://wasm/09f1a45a:wasm-function[1132]:0x74266)
    at il2cpp::os::File::Open(std::__2::basic_string<char, std::__2::char_traits<char>, std::__2::allocator<char>> const&, int, int, int, int, int*) (wasm://wasm/09f1a45a:wasm-function[1152]:0x74890)
    at dynCall_iiiiiii (wasm://wasm/09f1a45a:wasm-function[103808]:0x1a51aae)
    at afd4b7de-f946-49e2-85c5-3d0e823004de:999
    at invoke_iiiiiii (afd4b7de-f946-49e2-85c5-3d0e823004de:18412)
    at il2cpp::utils::DebugSymbolReader::LoadDebugSymbols() (wasm://wasm/09f1a45a:wasm-function[1297]:0x7bcba)
    at dynCall_i (wasm://wasm/09f1a45a:wasm-function[103801]:0x1a51a38)
    at afd4b7de-f946-49e2-85c5-3d0e823004de:999
```
Cause:

Missing function definition - doAccess() in SYSCALLS.

Workaround:

Add the following snippet to the `webgl.framework.js` in the `zip` file.

```javascript
var SYSCALLS = Module.StarkSYSCALLS = {...,
  doAccess: function(path, amode) {
    if (amode & ~7) {
      // need a valid mode
      return -28;
    }
    try {
      var lookup = FS.lookupPath(path, { follow: true });
      var node = lookup.node;
      if (!node) {
        return -44;
      }
      var perms = '';
      if (amode & 4) perms += 'r';
      if (amode & 2) perms += 'w';
      if (amode & 1) perms += 'x';
      if (perms /* otherwise, they've just passed F_OK */ && FS.nodePermissions(node, perms)) {
        return -2;
      }
      return 0;
    } catch (e) {
      if (typeof FS == 'undefined' || !(e.name === 'ErrnoError')) throw e;
      return -e.errno;
    }
  }
}
```

