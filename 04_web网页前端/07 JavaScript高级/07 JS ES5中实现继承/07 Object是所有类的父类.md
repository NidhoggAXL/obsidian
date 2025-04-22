**第一**：只要是对象就有隐式原型

**第二**：只要是函数也是对象，是一个函数对象，也有隐式原型

**第三**：原型也是一个对象，而原型对象的隐式原型会指向 Object 的显式原型

**第四**：Object 的显式原型对象的隐式原型指向 null

> 原型链的最高层是为 null，这样原型链就不会一直查找下去

```js
<script>
  //构造一个对象，让这个对象的显式原型指向构造这个对象的对象
  //构造出来的这个对象的显式原型指向函数的显式原型
  function creatObject(obj) {
    function F() {}
    F.prototype = obj
    return new F()
  }

  function inheritPrototype(subType, superType) {
    //通过 superType 构造出来的对象赋值给 subType 的显式原型
    subType.prototype = creatObject(superType.prototype)
    //让 subType 的原型里面 constructor 指向 subType
    //实际式让构成出来的那个对象显式原型中 constructor 指向 subType
    Object.defineProperty(subType.prototype, "constrcutor", {
      enumerable: false,
      configurable: true,
      writable: true,
      value: subType
    })
  }
  
  function Person() {}
  function Student() {}
  
  inheritPrototype(Student, Person)
  
  Object.prototype.message = "coderwhy"
  
  var stu = new Student()
  console.log(stu.message)//coderwhy
</script>
```

![gh](https://raw.githubusercontent.com/AXLflechazoPN/Obsidian/main/2024/173142170000074xbky.png)



