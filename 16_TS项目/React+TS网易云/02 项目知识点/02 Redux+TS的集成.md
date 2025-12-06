# 一、默认Redux的使用

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

# 二、state和dispatch问题

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

官方也获取 dispatch 类型：

```ts title="src/stores/index.ts"
export type AppDispath = typeof reduxStore.dispatch;
//  导出类型 AppDispath，它是从 reduxStore.dispatch 的类型中提取的 这种类型定义通常用于确保组件中的 dispatch 函数调用与 store 的 dispatch 具有相同的类型签名
```

类型有了，就是要封装自己的 Hooks 了：

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


action.payload 为 any 情况：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1763725258000b0eqwm.png)

# 三、action中的类型

> [!tip] 官方：
> 
> 所有生成 action 都应该使用 Redux Toolkit 中的 `PayloadAction<T>` 类型定义，该类型将 `action.payload` 字段的类型作为其通用参数。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1763725335000nrou17.png)

# 三、createAsyncThunk中的类型

```ts
export const getDataAction = createAsyncThunk("player/getData", (id, { getState }) => {
  console.log(id)
  // getState().player.playList 会报错
  // getState是一个 unknown 类型
})
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1764912971000weh8w4.png)

为什么会是一个 unknown 类型呢？在 redux 的默认ts中就是定义了 state 为 unknow 的类型。

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1764913239000499xkq.png)

要让 state = getState() 不是 unknow 不是 unknown 类型，那么就要设置类型，通过下面的方法设置：


```TS
// 为createAsyncThunk传入泛型
// 第一个泛型参数是createAsyncThunk的放回脂肪
// 第二个泛型参数是传入的 id 的类型
// 第三个泛型参数就是这是上面 AsyncThunkConfig 的类型，这里设置了里面的 state 的类型
export const getDataAction = createAsyncThunk<void, number, { state: RootState }>("player/getData", (id, { getState }) => {
  console.log(id)
  const data = getState().player.playList 
  console.log(data)
})
```

