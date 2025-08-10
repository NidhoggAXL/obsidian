# 一、Button组件解析

Button组件用于创建按钮，默认**块级元素**

常见属性：https://developers.weixin.qq.com/miniprogram/dev/component/button.html

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753583935000astjsp.png)


# 二、Button组件代码

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17535839610004omlvj.png)

# 三、open-type属性



<div style="
  height: 500px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753599122000us5twv.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>

## 3.1 获取用户的头像和名称

```html
<!-- index.wxml -->
<view class="container">
  <!-- 头像获取 -->
  <button open-type="chooseAvatar" bindchooseavatar="onChooseAvatar" class="avatar-btn">
    <image src="{{avatarUrl || '/images/default-avatar.png'}}" class="avatar" />
  </button>
  
  <!-- 昵称获取 - 优化为使用form表单 -->
  <form bindsubmit="submitUserInfo">
    <input 
      type="nickname"
      name="nickname"
      value="{{nickname}}"
      placeholder="请输入昵称"
      class="nickname-input"
    />
    
    <!-- 提交按钮 - 改为form表单提交 -->
    <button form-type="submit" class="submit-btn">提交信息</button>
  </form>
</view>
```

```js
// index.js
Page({
  data: {
    avatarUrl: '',
    nickname: ''
  },

  // 获取头像
  onChooseAvatar(e) {
    this.setData({ avatarUrl: e.detail.avatarUrl })
  },

  // 提交信息（通过表单提交）
  submitUserInfo(e) {
    // 从表单事件中获取昵称值
    const nickname = e.detail.value.nickname;
    
    // 更新数据并验证
    this.setData({ nickname }, () => {
      if (!this.data.avatarUrl || !this.data.nickname) {  // 使用 this.data.nickname
        wx.showToast({ title: '请完善信息', icon: 'none' })
        return;
      }
      
      // 实际提交逻辑 - 修复存储API使用方式
      wx.setStorage({
        key: 'userInfo',
        data: {
          avatar: this.data.avatarUrl,
          nickname: this.data.nickname
        },
        success: () => {
          // 提交成功后提示并跳转
          wx.showToast({ 
            title: '提交成功',
            icon: 'success',
            duration: 1500
          });
          
          // 延迟跳转让用户看到提示
          setTimeout(() => {
            wx.navigateBack()
          }, 1000);
        },
        fail: (err) => {
          console.error('存储失败:', err);
          wx.showToast({ title: '提交失败', icon: 'error' });
        }
      });
    });
  }
});
```

```css
/* index.wxss */
.container {
  padding: 40rpx;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.avatar-btn {
  padding: 0;
  background: transparent;
  border: none;
  width: 160rpx;
  height: 160rpx;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 60rpx;
}

.avatar {
  width: 100%;
  height: 100%;
}

form {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.nickname-input {
  width: 80%;
  padding: 20rpx;
  border-bottom: 1rpx solid #eee;
  margin-bottom: 60rpx;
}

.submit-btn {
  width: 70%;
  background: #07C160;
  color: white;
  border-radius: 50rpx;
}
```

1. **表单提交方式**：
    
    - 使用 `<form>` 包裹输入框和提交按钮
        
    - 通过 `form-type="submit"` 提交表单
        
    - 在 `submitUserInfo` 中通过 `e.detail.value` 获取所有表单值
        
2. **解决"使用微信昵称"问题**：
    
    - 直接通过表单提交事件获取昵称值
        
    - 确保点击"使用微信昵称"后能正确获取到值
        
    - 避免依赖 `bindinput` 或 `bindblur` 事件
        
3. **数据更新优化**：
    
    - 在提交时同时更新数据状态
        
    - 使用 setData 回调确保数据更新后执行验证
        
4. **布局改进**：
    
    - 优化表单元素布局
        
    - 增加间距提升视觉效果
        
    - 保持响应式设计
        
5. **保持合规性**：
    
    - 仍然使用官方要求的 `type="nickname"`
        
    - 符合微信小程序用户信息获取规范
 