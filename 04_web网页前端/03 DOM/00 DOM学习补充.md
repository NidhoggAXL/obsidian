# 一、动态列表输入案例
通过prompt接收用户的输入，根据输入创建一个列表

```js
<body>
  <ul class="list"></ul>
  <script>
    var ulEl = document.querySelector(".list")
    var isFlag = true
    
    while (isFlag) {
      var message = prompt("请输入")
      if (!message) {
        isFlag = false
      } else {
        var liEl = document.createElement("li")
        liEl.textContent = message
        ulEl.append(liEl)
      }
    }
  </script>
</body>
```

[[04 获取元素|querySelector]]  [[10 改变元素#一、创建元素|createElement]] [[05 Node节点属性#三、innerHTML、outerHTML、textContent|textContent]]

# 二、动态显示当前时间案例

```js
<body>
  <div class="time"></div>
  <script>
    var timeEl = document.querySelector(".time")

    function padLeft(content, count, padstr) {
      count = count || 2
      padstr = padstr || "0"
      content = String(content)
      return content.padStart(count, padstr)
    }
  
    setInterval(function() {
      var data = new Date()
      var year = data.getFullYear()
      var month = padLeft(data.getMonth())
      var day = padLeft(data.getDate())
      var hour = padLeft(data.getHours())
      var minute = padLeft(data.getMinutes())
      var second = padLeft(data.getSeconds())
      timeEl.textContent = `${year}-${month}-${day} ${hour}:${minute}:${second}`
    }, 1000);
  </script>
</body>
```


# 三、倒计时

```js
<body>
  <div class="box">
    <span class="item houer"></span>
    <span class="split">:</span>
    <span class="item minute"></span>
    <span class="split">:</span>
    <span class="item second"></span>
  </div>

  <script>
    //工具函数
    function padLeft(content, count, padstr) {
      count = count || 2
      padstr = padstr || "0"
      content = String(content)
      return content.padStart(count, padstr)
    }
  
    // 获取元素
    var houerEl = document.querySelector(".houer")
    var minuteEl = document.querySelector(".minute")
    var secondEl = document.querySelector(".second")
  
    // 设置距离时间
    var endData = new Date()
    endData.setHours(24)
    endData.setMinutes(0)
    endData.setSeconds(0)
    endData.setMilliseconds(0)
  
    setInterval (function() {
      var nowData = new Date()//获取当前时间
      //获取倒计时时间
      var intervalTime = Math.floor((endData.getTime() - nowData.getTime()) / 1000)
      
      // 对倒计时时间进行计算得到时分秒
      var houer = Math.floor(intervalTime / 3600)
      var minute = Math.floor(intervalTime / 60) % 60
      var second = intervalTime % 60
  
      // 把获取的时分秒设置到对应的地方
      houerEl.textContent = padLeft(houer)
      minuteEl.textContent = padLeft(minute)
      secondEl.textContent = padLeft(second)
    }, 1000)
  </script>
```



