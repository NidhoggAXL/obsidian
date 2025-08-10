在前面我们讲解过计算属性computed：当我们的某些属性是依赖其他状态时，我们可以使用计算属性来处理 

* 在前面的Options API中，我们是使用computed选项来完成的； 
* 在Composition API中，我们可以在 setup 函数中使用 computed 方法来编写一个计算属性；

如何使用computed呢？ 

* 方式一：接收一个getter函数，并为 getter 函数返回的值，返回一个不变的 ref 对象； 
* 方式二：接收一个具有 get 和 set 的对象，返回一个可变的（可读写）ref 对象；

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747558879000zzcgpb.png)

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/1747558883000gvfvwy.png)

