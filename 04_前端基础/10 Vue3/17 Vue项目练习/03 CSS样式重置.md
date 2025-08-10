对默认CSS样式进行重置: 

* normalize.css 
* reset.css
* common.css

**nomalize.css :**

* 前端别人编写好的样式重置文件，可以通过`npm install normalize.css`来进行下载到文件中.
* 再 main.js 来通过`import "normalize.css"`来引入

**reset.css:**

* 这个是自己再次添加的一些重置样式的CSS
* ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/17482661140002kud2t.png)

**common.css：** 

* 一些公共的CSS文件，比如字体、字号
* ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748266269000zxbw9w.png)


> [!tip] 这里的 reset.css 和 common.css 是否都再main里面引入呢?
> 如果这么做的话,就会造成 main.js 过于浮肿,不利于代码维护,这个时候就可以把这两个文件统一进行引入,统一到 index.css 里面引入其他两个文件
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748266470000mn2y2m.png)
> 最后的文件 css 文件格式如下:
> ![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748266514000mdik8c.png)

则main.js的引入:

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1748266633000hf089e.png)

> 两个是独立的css样式,所以就对两个都同时进行引入.



