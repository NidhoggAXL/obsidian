
```bash
npm install @mui/material @mui/styled-engine-sc styled-components
```

> [!warning] 使用 @metrail-UI必须设置 主题，如果不设置主题机会报错;

如果在使用 styled-compoents 的时候，如果使用了主题，那么就需要为两个设置主题，也可以通用一个主题

> [!note] 主题的本质
> metrail-ui的注意本质是使用 createTheme 来定义：
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1757148312000dimlz9.png)
> 
> styled-component的本质就是自定义数据：
> 
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1757148702000dk0rxh.png)

联合使用：

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/17571487410005rzmpm.png)

可以在 styled-components中使用 props 来获取两个主题的数据：

```js
import { boxShow } from "@/style/mixin";
import styled from "styled-components";

export const HeaderCenterWrapper = styled.div`
  color: ${props => props.theme.color.primaryColor}
  background-color: ${props => props.theme.palette.primary.main};
`
```


