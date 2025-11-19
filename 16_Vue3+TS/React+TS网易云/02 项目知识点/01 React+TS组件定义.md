# 一、函数式组件

## 正常函数组件

```tsx
import React, { memo } from 'react'

const discover = memo((props) => {
  return (
    <div>discover</div>
  )
})

export default discover 
```

## props类型约束

```tsx
import React, { memo } from 'react'

interface IPerson {
  name: string
  age?: number
}

const discover = memo((props: IPerson) => {
  return (
    <div>discover</div>
  )
})

export default discover 
```

## 函数组件实例约束

```tsx
import { memo } from "react"

interface IPerson {
  name: string
  age?: number
}

//简写
const Discover: React.FC<IPerson> = memo((props) => {
  return (
    <>
      <h1>{props.name}</h1>
      <h1>{props.age}</h1>
    </>
  )
})

//完整编写
// const Discover: React.FunctionComponent<IPerson> = memo((props) => {
//   return (
//     <>
//       <h1>{props.name}</h1>
//       <h1>{props.age}</h1>
//       <div>{props.children}</div>
//     </>
//   )
// })

export default Discover
```


> [!tip] 那么 FC 和 FunctionComponent 之间有什么关系呢？
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176354279100076ylhf.png)


## children类型约束

```tsx
<Discover name="axl" age={18}>
  {/* 可能是ReactElement */}
  <span>dlfjasdlkf</span>
  {/* 可能是REactElement数组 */}
  <span>哈哈哈</span>
  <span>哈哈哈</span>
  <span>哈哈哈</span>
  {/* 可能是string */}
  dlfjasl
</Discover>
```

因为 children 有许多的类型，类型很复杂，所以 react 提供了一个类型 ReactNode 。

```tsx
import { memo } from "react"
import type { ReactNode } from "react"

interface IPerson {
  name: string
  age?: number
  children?: ReactNode
}

const Discover: React.FC<IPerson> = memo((props) => {
  return (
    <>
      <h1>{props.name}</h1>
      <h1>{props.age}</h1>
      <div>{props.children}</div>
    </>
  )
})

export default Discover

```

> [!tip] 这个 ReactNode 到底是什么类型呢？
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/176354307000071ldsf.png)
 

