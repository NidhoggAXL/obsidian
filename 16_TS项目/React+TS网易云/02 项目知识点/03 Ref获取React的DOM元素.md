在 React 中获取组件的的DOM元素使用 `ElementRef` 来使用，例如获取 Carousel 的DOM 元素，如下面代码：

```jsx
import type { ElementRef } from "react"
const bannerRef = useRef<ElementRef<typeof Carousel>>(null)

<Carousel ref={bannerRef} />
```


