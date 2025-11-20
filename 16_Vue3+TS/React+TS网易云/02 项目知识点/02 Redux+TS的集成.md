
定义reducer：

```ts
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: {
    count: 0,
  },
  reducers: {
    increment: (state) => {
      state.count += 1;
    },
    decrement: (state) => {
      state.count -= 1;
    },
    incrementByAmount: (state, action) => {
      state.count += action.payload;
    }
  }
})

export const { increment, decrement, incrementByAmount } = counterSlice.actions
export default counterSlice.reducer
```

创建 Store：

```ts
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from './module/counter'

const reduxStore = configureStore({
  reducer: {
    counter: counterReducer
  }
})
```

使用 Store：

```tsx
const counte = useAppSelector(state => state.counter.count)

const dispatch = useAppDispatch()
const addCountBtnClick = () => {
  dispatch(increment())
}
```

> [!warning] 会报下面的错误！
> 并不知道 state 的类型，那个就算是 `state.counter.address` 也是不会报错误的，这样并不安全，并且没有提示，这里就需要修改代码，可以正确的推导出 state 的类型。
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1763608241000p7ihv3.png)


> [!abstract]
> 官方又说明需要如何做：https://cn.redux.js.org/tutorials/typescript-quick-start

首相获取 state ，可以通过 [[02 Redux的使用#二、Redux的使用过程|store.getState()]] 来获取，那么 state 的类型应该就是 store.getState() 的放回值类型，获取返回值类型可以使用 [[06 类型工具和类型体操#2.10 ReturnType`<Type>`|ReturnType`<Type>`]] 来获取。

```ts title="src/stores/index.ts"
export type RootState = ReturnType<typeof reduxStore.getState>;
/** 
 * 定义RootState类型，它通过获取Redux store的getState方法的返回类型来确定  
 * 这种方式可以确保RootState类型与实际store的状态结构保持同步 
 * 当store状态结构发生变化时，TypeScript会自动更新RootState类型 
*/
```

官方也给了获取 dispatch 类型：

```ts title="src/stores/index.ts"
export type AppDispath = typeof reduxStore.dispatch;
//  导出类型 AppDispath，它是从 reduxStore.dispatch 的类型中提取的 这种类型定义通常用于确保组件中的 dispatch 函数调用与 store 的 dispatch 具有相同的类型签名
```

类型有了，就是要封装自己的 Hooks了：

```ts title="src/hooks/app.ts"
import type { AppDispath, RootState } from "@/stores/redux"
import { useDispatch, useSelector, type TypedUseSelectorHook } from "react-redux"

export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector
/**
 * 自定义Hook：useAppSelector
 * 使用TypeScript类型化的useSelector钩子，用于从Redux store中获取状态
 *  @template RootState - 根状态的类型
 */

export const useAppDispatch: () => AppDispath = useDispatch
/**
 * 自定义Hook：useAppDispatch
 * 提供类型化的dispatch函数，用于触发Redux action
 * @returns {AppDispath} 返回类型化的dispatch函数
 */

```


使用的时候，使用自定义 Hook 就可以推导出 state 的正确类型啦：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17636089900004goebx.png)

	