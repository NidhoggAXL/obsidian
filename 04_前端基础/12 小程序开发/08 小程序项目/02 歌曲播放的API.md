
# 一、歌曲播放API 
[createInnerAudioContext](https://developers.weixin.qq.com/miniprogram/dev/api/media/audio/wx.createInnerAudioContext.html)

```js
	const innerAudioContext = wx.createInnerAudioContext({
  useWebAudioImplement: false // 是否使用 WebAudio 作为底层音频驱动，默认关闭。对于短音频、播放频繁的音频建议开启此选项，开启后将获得更优的性能表现。由于开启此选项后也会带来一定的内存增长，因此对于长音频建议关闭此选项
})
innerAudioContext.src = 'https://wx_test.mp3'

innerAudioContext.play() // 播放

innerAudioContext.pause() // 暂停

innerAudioContext.stop() // 停止

innerAudioContext.destroy() // 释放音频资源
```

用这个 API 创建出来的实例，或者说在什么时候创建出来呢？

分析：

 - 音乐播放是可以进行后台播放的，那么不可以只属于那一个页面。

# 二、歌曲播放实例的属性和方法

[innerAudioContext](https://developers.weixin.qq.com/miniprogram/dev/api/media/audio/InnerAudioContext.html)

常见的属性：

- src - 歌曲播放的源
	- 网易云播放的源URL：https://music.163.com/song/media/outer/url?id=歌曲id.mp3
- autoplay - 自动播放，默认为false
- currentTime - 当前播放的时间，实时变化的
- duration - 歌曲的持续时间（完整时间）

> [!warning] 获取duration的注意事项
> 在刚刚为到播放实例设置源(src)的时候是获取不到 duration ，会为 0