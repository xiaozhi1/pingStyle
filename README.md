### 1.请用两种方案实现一个品字整屏布局
代码： https://github.com/xiaozhi1/pingStyle
演示：
1.https://xiaozhi1.github.io/pingStyle/index.html
2.https://xiaozhi1.github.io/pingStyle/index2.html


### 2.请实现一个rem布局，要求在PC端缩放浏览器窗口大小时能够自动适配
```
function htmlFontSize() {
  var w = Math.max(document.documentElement.clientWidth, window.innerWidth || 0)
  var width = w > 720 ? 720 : w
  var fz = ~~(width * 100000 / 36) / 10000
  var html = document.getElementsByTagName('html')[0]
  html.style.cssText = 'font-size: ' + fz + 'px'
  var realfz = ~~(+window.getComputedStyle(html).fontSize.replace('px', '') * 10000) / 10000
  if (fz !== realfz) {
    html.style.cssText = 'font-size: ' + fz * (fz / realfz) + 'px'
  }
}
htmlFontSize()
window.onresize = function () { 
  htmlFontSize() 
}
```

### 3.请实现一个节流函数，并阐述节流函数的作用，并列举节流函数应用场景
```
const throttle = (fn, wait = 50) => {
  let previous = 0
  return function(...args) {
    let now = +new Date()
    if (now - previous > wait) {
      previous = now
      fn.apply(this, args)
    }
  }
}
const betterFn = throttle(() => console.log('fn 函数执行了'), 1000)
console.log(betterFn)
setInterval(betterFn, 1000)
```
作用：防止一段时间内频繁触发
场景：用户不断点击按钮触发接口请求，在n秒内只发送一次接口请求，不重复发送同样的接口





### 4.请用代码写出(今天是星期 x)其中 x 表示当天是星期几,如果当天是星期一,输出应该是"今天是星期一"
```
function NumberToString(number) {
  let string = ""
  switch (number) {
      case 0:
        string = '日'
          break
      case 1:
        string = '一'
          break
      case 2:
        string = '二'
          break
      case 3:
        string = '三'
        break
      case 4:
        string = '四'
        break
      case 5:
        string = '五'
          break
      case 6:
        string = '六'
          break
      default: 
        string = ''
          break
  }
  return string
}
const birthday = new Date('2020-03-16');
const day = birthday.getDay();
const msg = '今天是星期'+ NumberToString(day)
console.log(msg)
```

### 5.有一个大数组：var a = ['1', '2', '3', ...]，a 的长度是 100，内容填充随机整数的字符串。请先构造此数组 a，然后设计一个算法将其内容去重。
```
var a = Array(100)
for(var i=0;i<a.length;i++){
	a[i]= String(Math.floor(Math.random()*10))
}
var b = Array.from(new Set(a))
a = b
console.log(a)
```

### 6.实现一个add函数，让add(a)(b)和add(a,b)两种调用结果相同。
```
function add (a,b){
    if(b){
      return a+b
    }else{
       return function(b){
        return b + a;
    };
    }
}
console.log(add(1,3))
console.log(add(1)(3))
```

### 7.请实现超出整数存储范围的两个大整数相加 function add(a, b)。
```
const add = (...args) => {
    let _x = 0;
    for (let i of args) {
        _x = _x + Number(i)
    }
    let _y = _x >= 10 ? { m: 1, n: _x - 10 } : { m: 0, n: _x }
    return _y;
}
const addLength = (s1, num) => {
    return new Array(num + 1).join("0") + s1;
}
const merge = (s1, s2) => {
    s1 = s1.split("");
    s2 = addLength(s2, s1.length - s2.length).split("");
    let _t = 0,
        _str = "";
    for (var i = s1.length - 1; i >= 0; i--) {
        let z = add(s1[i], s2[i], _t);
        _str = z.n + _str
        _t = z.m;
    }
    if (_t == 1) _str = _t + _str;
    return _str;
}
const Main = (s1, s2) => {
    if (s1.length > s2.length) return merge(s1, s2);
    return merge(s2, s1)
}

```

### 8.请基于jQuery实现一个手风琴菜单
代码：  https://github.com/xiaozhi1/accordion
演示：  https://xiaozhi1.github.io/accordion/index.html



### 9.请用原生js实现一个自定义事件对象 UserEvent
```
class Event {
    constructor(initEventList = {}){
        this.eventList = initEventList
    }
    on(key,event){
        this.eventList[key] = event  
    }
    fire(key,...payload){
        this.eventList[key](...payload)
    }
    off(key){
        delete this.eventList[key]
    }
    one(key){
        this.eventList[key] = event 
        delete this.eventList[key]
    }
}
```

### 10.请实现一个图片轮播
代码：  https://github.com/xiaozhi1/slides-demo-1
演示：  https://xiaozhi1.github.io/slides-demo-1/index.html