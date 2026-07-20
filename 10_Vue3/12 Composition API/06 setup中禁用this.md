官方关于this有这样一段描述:

 - 表达的含义是this并没有指向当前组件实例;
 - 并且在setup被调用之前，data、computed、methods等都没有被解析;
 - 所以无法在setup中获取this;

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2025/1784363148000uvq3fc.png)




