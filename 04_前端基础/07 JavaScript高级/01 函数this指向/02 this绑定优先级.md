学习了四条规则，接下来开发中我们只需要去查找函数的调用应用了哪条规则即可，但是如果一个函数调用位置应用了多条规则，优先级谁更高呢?

1. 默认规则的优先级最低

* **毫无疑问**，默认规则的优先级是最低的，因为存在其他规则时，就会通过其他规则的方式来绑定this

```js
  <script>
    function fool() {
      console.log(this)//默认绑定
    }
  
    var demo = {
      name: 'axl',
      bar: fool//隐式绑定
    }

    //隐式绑定
    demo.bar()//{name: 'axl', bar: ƒ}
    //如果隐式高于默认就是Object
    //反之默认高于隐士就是Window
  </script>
```

2. 显示绑定优先级高于隐式绑定

```js
  <script>
    function fool() {
      console.log(this)
    }
  
    var demo = {
      name: "axl",
      bar: fool//隐士绑定
    }

    //显示绑定
    demo.bar.apply("aaa")//String {'aaa'}
  </script>
```


3. new绑定优先级高于隐式绑定

```js
  <script>
    function fool() {
      this.age = 18
      console.log(this)//默认绑定
    }
  
    var demo = {
      name: "axl",
      bar: fool//隐式绑定
    }

    //new调用
    new fool()//fool {age: 18}
  </script>
```

4. new绑定优先级高于bind

* new绑定和call、apply是**不允许同时使用**的，所以**不存在谁的优先级更高**
* new绑定可以和bind一起使用，**new绑定优先级更高**

```js
  <script>
    function fool() {
      this.name = "axl"
      console.log(this)//默认绑定
    }

    //bind绑定
    var demo = fool.bind("haha")
    demo()//String {'haha', name: 'axl'}
    
    //new绑定
    new demo()//fool {name: 'axl'}
  </script>
```


5. 显示绑定中bind优先级高于call、apply

```js
  <script>
    function fool() {
      console.log(this)//默认绑定
    }

    //显示bind绑定
    var box = fool.bind("bbb")
    box()//String {'bbb'}
  
    //显示apply、call绑定
    // box.apply("aaa")//String {'bbb'}
    box.call("aaa")//String {'bbb'}
  </script>
```