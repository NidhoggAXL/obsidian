# 一、Next.js 16(App Router)

在 Next.js 16 (App Router) 中集成 Redux 与 Pages Router 有所不同，核心挑战在于：

1. **Store 必须是请求级别的**：Next.js 服务器会同时处理多个请求，Store 不能是全局单例，否则会跨请求污染数据 [](https://redux.js.org/usage/nextjs)。
2. **Server Components 不能直接访问 Redux**：RSCs 无法使用 React Context 和 Hooks，所以不能直接在 Server Component 中读取或写入 Store [](https://redux.js.org/usage/nextjs)。
3. **Provider 必须是 Client Component**：任何与 Redux 交互的组件（包括 Provider）都必须是客户端组件 [](https://redux.js.org/usage/nextjs)[](https://dev.to/devtush/setting-up-redux-toolkit-in-nextjs-38k9#comments)。

# 二、快速开始（官方推荐方式）

使用官方 with-redux 模板

```bash
npx create-next-app --example with-redux my-app
```

这会自动生成一个已配置好 Redux Toolkit 和 React-Redux 的 Next.js 项目，包含 Counter 示例 [](https://react-redux.js.org/introduction/getting-started?source=post_page-----5bbf09c3d483---------------------------------------)[](https://gitcode.com/gh_mirrors/rea/react-redux?utm_source=gitcode_repo_files&from_link=c84a07454254c934e6197a3cb323f3f3)[](https://react.redux.js.cn/introduction/getting-started#help-and-discussion)。

# 三、手动集成（完整 TypeScript 示例）

## 2.1 安装依赖

```bash
npm install @reduxjs/toolkit react-redux
npm install -D @types/react-redux   # TypeScript 类型（如需要）
```


## 2.2 目录结构

```text
src/
├── app/
│   ├── layout.tsx          # 根布局
│   └── StoreProvider.tsx   # Redux Provider（Client Component）
├── lib/
│   ├── store.ts            # Store 配置（makeStore 函数）
│   ├── hooks.ts            # 类型化的 hooks
│   └── features/
│       └── counter/
│           └── counterSlice.ts
```

## 2.3 创建 Slice

```ts
// lib/features/counter/counterSlice.ts
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface CounterState {
  value: number;
}

const initialState: CounterState = {
  value: 0,
};

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action: PayloadAction<number>) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default counterSlice.reducer;
```

## 2.4 配置 Store

```ts
// lib/store.ts
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './features/counter/counterSlice';

// 创建 store 的函数，每个请求调用一次
export const makeStore = () => {
  return configureStore({
    reducer: {
      counter: counterReducer,
    },
  });
};

// 类型推断
export type AppStore = ReturnType<typeof makeStore>;
export type RootState = ReturnType<AppStore['getState']>;
export type AppDispatch = AppStore['dispatch'];
```

## 2.5 创建类型化 Hooks

```ts
// lib/hooks.ts
import { useDispatch, useSelector, useStore } from 'react-redux';
import type { AppDispatch, AppStore, RootState } from './store';

// 在整个应用中使用这些类型化的 hooks，而不是普通的 useDispatch/useSelector
export const useAppDispatch = useDispatch.withTypes<AppDispatch>();
export const useAppSelector = useSelector.withTypes<RootState>();
export const useAppStore = useStore.withTypes<AppStore>();
```

## 2.6 创建 Provider 组件

```tsx
// app/StoreProvider.tsx
'use client';

import { useRef } from 'react';
import { Provider } from 'react-redux';
import { makeStore, AppStore } from '@/lib/store';

export default function StoreProvider({children,}: {children: React.ReactNode;
}) {
  const storeRef = useRef<AppStore | null>(null);
  
  // 确保 store 只创建一次
  if (!storeRef.current) {
    storeRef.current = makeStore();
  }

  return <Provider store={storeRef.current}>{children}</Provider>;
}
```

## 2.7 在根布局中集成

```tsx
// app/laytout.tsx
import { Inter } from 'next/font/google';
import StoreProvider from './StoreProvider';
import './globals.css';

const inter = Inter({ subsets: ['latin'] });

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="zh-CN">
      <body className={inter.className}>
        <StoreProvider>{children}</StoreProvider>
      </body>
    </html>
  );
}
```


## 2.8 在组件中使用

```tsx
'use client';

import { useAppSelector, useAppDispatch } from '@/lib/hooks';
import { increment, decrement } from '@/lib/features/counter/counterSlice';

export default function Counter() {
  const count = useAppSelector((state) => state.counter.value);
  const dispatch = useAppDispatch();

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => dispatch(decrement())}>-</button>
      <button onClick={() => dispatch(increment())}>+</button>
    </div>
  );
}
```

# 四、高级配置

初始化 Store 数据（如从 Server Component 传递数据）

```tsx
// app/StoreProvider.tsx
'use client';

import { useRef } from 'react';
import { Provider } from 'react-redux';
import { makeStore, AppStore } from '@/lib/store';
import { setInitialCount } from '@/lib/features/counter/counterSlice';

export default function StoreProvider({
  count,  // 从 Server Component 传入的数据
  children,
}: {
  count: number;
  children: React.ReactNode;
}) {
  const storeRef = useRef<AppStore | null>(null);
  
  if (!storeRef.current) {
    storeRef.current = makeStore();
    // 初始化 store 数据
    storeRef.current.dispatch(setInitialCount(count));
  }

  return <Provider store={storeRef.current}>{children}</Provider>;
}
```

使用 Redux Persist（持久化存储）:

```bash
npm install redux-persist
```

```ts
// lib/store.ts
import { configureStore, combineReducers } from '@reduxjs/toolkit';
import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage';
import counterReducer from './features/counter/counterSlice';

const persistConfig = {
  key: 'root',
  storage,
};

const rootReducer = combineReducers({
  counter: counterReducer,
});

const persistedReducer = persistReducer(persistConfig, rootReducer);

export const makeStore = () => {
  return configureStore({
    reducer: persistedReducer,
    middleware: (getDefaultMiddleware) =>
      getDefaultMiddleware({
        serializableCheck: false, // 必须禁用，因为 redux-persist 使用了非序列化的值
      }),
  });
};

export const persistor = persistStore(makeStore());
```


然后在 Provider 中包裹 `PersistGate`：

```tsx
'use client';

import { PersistGate } from 'redux-persist/integration/react';
import { persistor, makeStore } from '@/lib/store';

export default function StoreProvider({ children }) {
  const storeRef = useRef(null);
  if (!storeRef.current) {
    storeRef.current = makeStore();
  }

  return (
    <Provider store={storeRef.current}>
      <PersistGate loading={null} persistor={persistor}>
        {children}
      </PersistGate>
    </Provider>
  );
}
```


# 四、关键注意事项

| 要点                                | 说明                                                                                                                                                                |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Provider 必须是 Client Component** | 必须添加 `'use client'` 指令，因为 Redux 依赖 React Context [](https://redux.js.org/usage/nextjs)[](https://dev.to/devtush/setting-up-redux-toolkit-in-nextjs-38k9#comments) |
| **Store 按请求创建**                   | 使用 `makeStore()` 函数而非全局单例，避免请求间数据污染 [](https://redux.js.org/usage/nextjs)                                                                                         |
| **Server Components 不访问 Redux**   | RSCs 无法使用 `useSelector`/`useDispatch`，只能在 Client Components 中使用                                                                                                   |
| **使用类型化 Hooks**                   | `useAppDispatch`、`useAppSelector` 提供完整 TypeScript 支持 [](https://dev.to/devtush/setting-up-redux-toolkit-in-nextjs-38k9#comments)                                  |
| **SSR 兼容性**                       | 使用 `useRef` 确保 store 只在客户端创建一次，避免服务端渲染时的内存泄漏 [](https://redux.js.org/usage/nextjs)                                                                                |

## 五、常见问题

### Q: 为什么不能用全局 store？

A: Next.js 服务器会同时处理多个请求。如果 store 是全局单例，不同请求的用户数据会相互污染。必须为每个请求创建独立的 store 实例 [](https://redux.js.org/usage/nextjs)。

### Q: 能否在 Server Component 中使用 Redux？

A: **不能**。Server Components 无法使用 React Context 和 Hooks，因此无法直接读取或写入 Redux store。数据获取应在 Server Component 中直接使用 `fetch`，然后通过 props 传递给子组件 [](https://redux.js.org/usage/nextjs)。

### Q: Redux 适合在 Next.js 中存储什么数据？

A: 推荐只存储**可变的、全局的客户端状态**（如用户认证状态、UI 主题、购物车）。对于服务器端数据，优先使用 Next.js 内置的 `fetch` 缓存和 Server Components [](https://redux.js.org/usage/nextjs)。

