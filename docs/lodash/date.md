## 当前时间

### now
> 返回当前的毫秒值

```javascript
_.now();
```

```javascript
_.defer(function(stamp) {
  console.log(_.now() - stamp);
}, _.now());
// => 记录延迟函数调用的毫秒数
```