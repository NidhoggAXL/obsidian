# 一、小程序的样式写法

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753615307000c2lyii.png)

# 二、WXSS支持的选择器

<div style="
  height: 500px; 
  overflow-y: auto;
  background: #fafafa;
">
  <img 
    src="https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753615127000yhzynr.png" 
    style="
      width: 100%;
      display: block;
      border-radius: 4px;
    "
  />
</div>

# 三、WXSS优先级与CSS类似

权重如图:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753615343000tqml4w.png)

# 四、wxss的扩展
## 4.1 尺寸单位

- rpx（responsive pixel）: 可以根据屏幕宽度进行自适应。规定屏幕宽为750rpx。
- 如在 iPhone6 上，屏幕宽度为375px，共有750个物理像素，则750rpx = 375px = 750物理像素，1rpx = 0.5px = 1物理像素。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1753616248000a9750p.png)

> [!tip] **建议：** 开发微信小程序时设计师可以用 iPhone6 作为视觉稿的标准。

> [!warning] **注意：** 在较小的屏幕上不可避免的会有一些毛刺，请在开发时尽量避免这种情况。

