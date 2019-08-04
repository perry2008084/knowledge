
## 节流

节流的概念是，在指定时间段内限制函数的调用。

原理是，通过一个闭包和标记，在闭包中记录可运行的标记状态，如果当前不可运行则直接返回，否则会启用一个定时器，定时特定时间后运行函数。

实现:

```javascript
function throttle(fn, interval = 300) {
  var canRun = true;

  return function() {
    if (!canRun) return;
    canRun = false;

    setTimeout(() => {
      fn.apply(this, arguments);
      canRun = true;
    }, interval);
  }
}
```

## 防抖

防抖的概念是，在任务频繁发生的情况下，只有当达到特定的时间间隔时才触发。

原理是， 通过闭包记录定时器的返回句柄，如果未达到时间间隔，则清除定时器，否则执行相应函数。

实现：

```javascript
function debounce(fn, interval = 300) {
  var timer = null;
  return function() {
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(this, arguments);
    }, interval);
  }
}
```

## 参考
* [函数节流与函数防抖](https://juejin.im/entry/58c0379e44d9040068dc952f)