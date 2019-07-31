## 限制

### debounce（防抖动，间隔调用）
> 返回新函数

```javascript
_.debounce(func, [wait=0], [options={}]);
```
```javascript
// 避免窗口在变动时出现昂贵的计算开销。
jQuery(window).on('resize', _.debounce(calculateLayout, 150));
 
// 当点击时 `sendMail` 随后就被调用。
jQuery(element).on('click', _.debounce(sendMail, 300, {
  'leading': true,
  'trailing': false
}));
 
// 确保 `batchLog` 调用1次之后，1秒内会被触发。
var debounced = _.debounce(batchLog, 250, { 'maxWait': 1000 });
var source = new EventSource('/stream');
jQuery(source).on('message', debounced);
 
// 取消一个 trailing 的防抖动调用
jQuery(window).on('popstate', debounced.cancel);
```

### throttle（节流，时间内最多执行一次）

```javascript
_.throttle(func, [wait=0], [options={}])
```
```javascript
// 避免在滚动时过分的更新定位
jQuery(window).on('scroll', _.throttle(updatePosition, 100));
 
// 点击后就调用 `renewToken`，但5分钟内超过1次。
var throttled = _.throttle(renewToken, 300000, { 'trailing': false });
jQuery(element).on('click', throttled);
 
// 取消一个 trailing 的节流调用。
jQuery(window).on('popstate', throttled.cancel);
```

### once（只能执行一次的函数，缓存结果）
> 返回新函数

```javascript
// 返回一个只能执行一次的函数
// 若再次调用，将立刻返回第一次的返回值
_.once(func);
```
```javascript
var initialize = _.once(createApplication);
initialize();
initialize();
// `initialize` 只能调用 `createApplication` 一次。
```

### before（限制调用次数，缓存结果）
> 返回新函数

```javascript
// 不超过 n 次调用
// 之后如果再调用
// 则返回最后一次的返回值
_.before(n, func)
````
```javascript
jQuery(element).on('click', _.before(5, addContactToList));
// => allows adding up to 4 contacts to the list
```

### after（调用 n 次后，才会触发）
> 返回新的函数

```javascript
// 传入 次数 和 回调
// 触发 n 此后，触发回调
// 返回新函数
_.after(n, func);
```
```javascript
var saves = ['profile', 'settings'];
 
var done = _.after(saves.length, function() {
  console.log('done saving!');
});
 
_.forEach(saves, function(type) {
  asyncSave({ 'type': type, 'complete': done });
});
// => Logs 'done saving!' after the two async saves have completed.
```

### unary（限制参数为一个，忽略其他）

```javascript
_.unary(func);
```
```javascript
_.map(['6', '8', '10'], _.unary(parseInt));
// => [6, 8, 10]
```

### ary（限制传入的参数数量，忽略其他）
> 返回新函数

```javascript
_.ary(func, [n=func.length])
```
```javascript
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// => [6, 8, 10]
```

### curry（传入的参数齐全后，才会调用）
> 返回新函数

```javascript
_.curry(func, [arity=func.length])
```
```javascript
var abc = function(a, b, c) {
  return [a, b, c];
};
 
var curried = _.curry(abc);
 
curried(1)(2)(3);
// => [1, 2, 3]
 
curried(1, 2)(3);
// => [1, 2, 3]
 
curried(1, 2, 3);
// => [1, 2, 3]
 
// Curried with placeholders.
curried(1)(_, 3)(2);
// => [1, 2, 3]
```

### curryRight（同 curry，参数反向传入）

```javascript
_.curryRight(func, [arity=func.length]);
```
```javascript
var abc = function(a, b, c) {
  return [a, b, c];
};
 
var curried = _.curryRight(abc);
 
curried(3)(2)(1);
// => [1, 2, 3]
 
curried(2, 3)(1);
// => [1, 2, 3]
 
curried(1, 2, 3);
// => [1, 2, 3]
 
// Curried with placeholders.
curried(3)(1, _)(2);
// => [1, 2, 3]
```

## 取反函数

### negate（将断言函数取反）
> 返回新函数

```javascript
// 传入一个返回断言的函数
// 返回一个取反的函数
_.negate(predicate);
```
```javascript
function isEven(n) {
  return n % 2 === 0;
}
 
_.filter([1, 2, 3, 4, 5, 6], _.negate(isEven));
// => [1, 3, 5]
```

## 延迟调用

### defer（当前堆栈清理完毕后调用）
> 返回新函数

```javascript
_.defer(func, [args])
```
```javascript
_.defer(function(text) {
  console.log(text);
}, 'deferred');
// => 一毫秒或更久一些输出 'deferred'。
```

### delay（延迟 wait 毫秒后，调用）
> 返回新函数

```javascript
_.delay(func, wait, [args])
```
```javascript
_.delay(function(text) {
  console.log(text);
}, 1000, 'later');
// => 一秒后输出 'later'。
```

## 缓存

### memoize（根据 key 缓存结果）
> 返回新函数

```javascript
// 创建一个会缓存 func 结果的函数
// 默认情况内部会把 func 的第一个参数作为 key 进行缓存
// 如果提供了 resolver
// 就用 resolver 的返回值作为 key 缓存函数的结果
// resolver 的第一个参数为 func 的参数
_.memoize(func, [resolver]);
```
```javascript
var object = { 'a': 1, 'b': 2 };
var other = { 'c': 3, 'd': 4 };
 
var values = _.memoize(_.values);
values(object);
// => [1, 2]
 
values(other);
// => [3, 4]
 
object.a = 2;
values(object);
// => [1, 2]
 
// 修改结果缓存。
values.cache.set(object, ['a', 'b']);
values(object);
// => ['a', 'b']
 
// 替换 `_.memoize.Cache`。
_.memoize.Cache = WeakMap;
```

## 参数处理

### spread（调用时将数组参数拆分）
> 返回新函数

```javascript
// 返回一个需要传入数组参数的函数
// func 调用时将会拆分参数数组
// Promise.all 很有用
_.spread(func, [start=0]);
```
```javascript
var say = _.spread(function(who, what) {
  return who + ' says ' + what;
});
 
say(['fred', 'hello']);
// => 'fred says hello'
 
var numbers = Promise.all([
  Promise.resolve(40),
  Promise.resolve(36)
]);
 
numbers.then(_.spread(function(x, y) {
  return x + y;
}));
// => a Promise of 76
```

### partial（正向预设参数）
> 返回新函数

```javascript
// 返回一个调用 func 并传入预设的 partials 参数的函数
// 这个方法类似 _.bind，除了它不会绑定 this。 
// 可以传入 _ 当做占位符
// 调整调用新函数时的参数顺序
_.partial(func, [partials]);
```
```javascript
var greet = function(greeting, name) {
  return greeting + ' ' + name;
};
 
var sayHelloTo = _.partial(greet, 'hello');
sayHelloTo('fred');
// => 'hello fred'
 
// 使用了占位符。
var greetFred = _.partial(greet, _, 'fred');
greetFred('hi');
// => 'hi fred'
```

### partialRight（反向预设参数）
> 返回新函数

```javascript
// 相比 partial 参数顺序是反向的
_.partialRight(func, [partials])
```
```javascript
var greet = function(greeting, name) {
  return greeting + ' ' + name;
};
 
var greetFred = _.partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'
 
// 使用了占位符。
var sayHelloTo = _.partialRight(greet, 'hello', _);
sayHelloTo('fred');
// => 'hello fred'
```

### flip（接收翻转顺序的参数）
> 返回新函数

```javascript
_.flip(func);
```
```javascript
var flipped = _.flip(function() {
  return _.toArray(arguments);
});
 
flipped('a', 'b', 'c', 'd');
// => ['d', 'c', 'b', 'a']
```

### rearg（调整参数位置）
> 返回新函数

```javascript
// 根据 indexes
// 调用 func 时，调整参数位置
_.rearg(func, indexes);
```
```javascript
var rearged = _.rearg(function(a, b, c) {
  return [a, b, c];
}, [2, 0, 1]);
 
rearged('b', 'c', 'a')
// => ['a', 'b', 'c']
```

## this 绑定

### bind
> 返回新函数

```javascript
// 第三个参数为附加参数
// 调用时，默认将第三个参数靠前，调用时传入的靠后
// 可传入 _ 当做占位符
// 改变传入参数的顺序
_.bind(func, thisArg, [partials]);
```
```javascript
var greet = function(greeting, punctuation) {
  return greeting + ' ' + this.user + punctuation;
};
 
var object = { 'user': 'fred' };
 
var bound1 = _.bind(greet, object, 'hi');
bound1('!');
// => 'hi fred!'
 
// Bound with placeholders.
var bound2 = _.bind(greet, object, _, '!');
bound2('hi');
// => 'hi fred!'
```

### bindKey
> 返回新函数

```javascript
// 和 bind 类似
// 绑定一个 key 值
// 对应的 value 应该为一个函数
// 函数可以在其定以后，再次更改
_.bindKey(object, key, [partials]);
```
```javascript
var object = {
  'user': 'fred',
  'greet': function(greeting, punctuation) {
    return greeting + ' ' + this.user + punctuation;
  }
};
 
var bound = _.bindKey(object, 'greet', 'hi');
bound('!');
// => 'hi fred!'
 
object.greet = function(greeting, punctuation) {
  return greeting + 'ya ' + this.user + punctuation;
};
 
bound('!');
// => 'hiya fred!'
 
// Bound with placeholders.
var bound = _.bindKey(object, 'greet', _, '!');
bound('hi');
// => 'hiya fred!'
```

## 没有整理的
> 存在即合理，感觉没卵用....
```javascript
_.overArgs(func, [transforms=[_.identity]]);

_.rest(func, [start=func.length-1]);
```