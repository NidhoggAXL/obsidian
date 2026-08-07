# 手动路由的跳转

目前我们实现的跳转主要是通过[[02 Router的基本使用#三、路由配置和跳转|Link或者NavLink]]进行跳转的，实际上也可以通过JavaScript代码进行跳转。 

- 我们知道Navigate组件是可以进行路由的默认跳转的，但是**依然是组件的方式**。 
- 如果希望通过JavaScript代码逻辑进行跳转（比如点击了一个button），那么就**需要获取到navigate对象**。 

**在Router6.x版本之后，代码类的API都迁移到了hooks的写法：** 

- 如果希望进行代码跳转，需要通过 useNavigate 的Hook获取到 **navigate对象** 进行操作； 
- 那么如果是一个函数式组件，可以直接调用，但是如果是一个类组件呢？

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17556926590009pu1eg.png)

## 函数组件

```jsx
import { useNavigate } from 'react-router-dom';

function MyFunctionComponent() {
  //Hooks必须放到顶层作用域，不可以包裹
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/target-path');
  };

  return <button onClick={handleClick}>跳转</button>;
}
```

## 类组件

1. **创建高阶组件（HOC）**：封装 `useNavigate` Hook，将其传递给类组件。
    
2. **通过 props 调用跳转**：

```jsx
// 1. 创建高阶组件
import { useNavigate } from 'react-router-dom';

export function withRouter(Component) {
  return (props) => {
    const navigate = useNavigate();
    return <Component {...props} navigate={navigate} />;
  };
}

// 2. 类组件中使用
import React from 'react';
import { withRouter } from './withRouter'; // 自定义 HOC

class MyComponent extends React.Component {
  handleClick = () => {
    this.props.navigate('/target-path'); // 通过 props 调用
  };

  render() {
    return <button onClick={this.handleClick}>跳转</button>;
  }
}

export default withRouter(MyComponent);
```





