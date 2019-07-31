## 链式调用
> 处理复杂的数据转换 <br/>
> 优化代码，提高阅读性

## 注意
> 惰性并不好用... <br/>
> 若是原始类型，那么值不能改，改了也没用 <br/>
> 若是引用类型，那么引用指针不能改，改了也没用...

## 隐式调用
> 结尾必须是返回原始值或唯一值的函数 <br/>
> 才会自动执行整个链条函数（value 函数） <br/>
> 否则必须调用 value 结束链条（惰性调用） <br/>

```javascript
let arr = [1, 2, 3];

_(arr)
  .map(num => num * num)
  .sum();
// => 14

_(arr)
  .map(num => num * num)
  .thru(num => num[1])
  .value();
// => 14
```

## 显式调用
> 结尾必须是 value 函数 <br/>
> 显式的结束整个链条 <br/>
> 个人通常用这个比较多...感觉比隐式明确些

```javascript
let arr = [];

let handler = _
  .chain(arr)
  .map(num => num * num)
  .sum();

// 这里如果是 arr = [1, 2, 3, 4];
// 引用指针发生了变化，会计算异常
arr.push(1, 2, 3, 4);

console.log(handler.value());
```