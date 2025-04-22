# 一、堆属性操作的控制
在前面我们的属性都是直接定义在对象内部，或者直接添加到对象内部的:

* 但是这样来做的时候我们就不能对这个属性进行一些限制:
* 比如这个属性是否是可以通过delete删除的?
* 这个属性是否在for in遍历的时候被遍历出来呢?

```js
var obj = {
  name: "axl",
  height: 18
}
```

如果我们想要对一个属性进行比较精准的操作控制，那么我们就可以使用**属性描述符**

* 通过属性描述符可以精准的添加或修改对象的属性;
* 属性描述符需要使用 Object.defineProperty 来对属性进行添加或者修改;

# 二、Object.defineProperty
Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。

```js
Object.defineProperty(obj, prop, descriptor)
```

可接收三个参数

* obj要定义属性的对象;
* prop要定义或修改的属性的名称或 Symbol;
* descriptor要定义或修改的属性描述符

返回值:

* 被传递给函数的对象。

# 三、属性描述符分类

## 3.1 数据属性描述符
数据数据描述符有如下四个特性:

**Configurable(可配置)**:表示属性是否可以通过delete删除属性，是否可以修改它的特性或者是否可以将它**修改为存取属性描述符**;

* 当我们直接在一个对象上定义某个属性时，这个属性的Configurable为true;

```js
<script>
  var obj = {
    name: "axl"
    //name默认configurable为ture
    //可以进修修改
  }
  
  delete obj.name
  console.log(obj)//{}
</script>
```


* 当我们通过属性描述符定义一个属性时，这个属性的Configurable默认为false;

```js
<script>
  var obj = {
    name: "axl"
    //name默认configurable为ture
    //可以进修修改
  }
  
  Object.defineProperty(obj, "height", {})
  //通过属性描述符定义的height默认为false
  //是不可以修改的
  delete obj.height
  console.log(obj)//{name: 'axl', height: undefined}
  //height还在，不可以进行delete操作
</script>
```

**Enumerable(可枚举)**:表示属性是否可以通过for-in或者Object.keys()返回该属性

* 当我们直接在一个对象上定义某个属性时，这个属性的Enumerable为true;
* 当我们通过属性描述符定义一个属性时，这个属性的Enumerable默认为false;

```js
<script>
  var obj = {
    name: "axl",
    age: 18
  }
  
  Object.defineProperty(obj, "age", {
    enumerable: false//age 是不可以遍历的
  })
  console.log(Object.keys(obj))//['name']
</script>
```

**Writable(可写的)**:表示是否可以修改属性的值;

* 当我们直接在一个对象上定义某个属性时，这个属性的Writable为true;
* 当我们通过属性描述符定义一个属性时，这个属性的Writable默认为false;

```js
<script>
  var obj = {
    name: "axl",
    age: 18
  }

  Object.defineProperty(obj, "age", {
    writable: false//不可以写入
  })
  
  obj.age = 20//无效，严格模式下会报错
  console.log(obj.age)//18
</script>
```


**value**:属性的value值，读取属性时会返回该值，修改属性时，会对其进行修改;

* 默认情况下这个值是undefined;

```js
<script>
  var obj = {
    name: "axl",
    age: 10
  }

//默认查看
  console.log(obj.age.value)//undefined

  Object.defineProperty(obj, "age", {
    value: "18"//修改age的值
  })

  //读取属性返回value
  console.log(obj.age)//18
  
  //修改
  obj.age = 20
  console.log(obj.age)//20
</script>
```


## 3.2 存取属性描述符
Configurable：

* 和数据属性描述符一致

Enumerable：

* 和数据属性描述符一致

Get：获取属性时会执行的函数。默认undefined

Set：设置属性时会执行的函数。默认undefined

```js
<script>
  var obj = {
    name: "axl"
  }
  
  //记录获取属性时的数据
  var _name = ""
  Object.defineProperty(obj, "name", {
    set: function(value) {
      console.log("执行了set函数",value)
      _name = value
    },
    get: function() {
      console.log("执行了get函数")
      return _name
    }
  })
  
  //设置属性时
  obj.name = "coder"
  //执行了set函数 coder
  obj.name = "mba"
  //执行了set函数 mba
  
  //获取属性时
  console.log(obj.name)
  //执行了get函数
  //mba
</script>
```


