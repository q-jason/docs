## lodash 强大的迭代器

### iteratee（强大）
> 返回新函数

```javascript
// 新函数需要传入一个对象

// 若 func 是字符串
// 则返回对象所对应的属性

// 若 func 是数组
// 则把数组
// 第一个元素作为 key
// 第二个元素作为 value（浅比较）
// 进行比较
// 返回 true 或 false

// 若 func 是个对象
// 则进行深度比较
// 返回 true 或 false
_.iteratee([func=_.identity]);
```
```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];
 
// The `_.matches` iteratee shorthand.
_.filter(users, _.iteratee({ 'user': 'barney', 'active': true }));
// => [{ 'user': 'barney', 'age': 36, 'active': true }]
 
// The `_.matchesProperty` iteratee shorthand.
_.filter(users, _.iteratee(['user', 'fred']));
// => [{ 'user': 'fred', 'age': 40 }]
 
// The `_.property` iteratee shorthand.
_.map(users, _.iteratee('user'));
// => ['barney', 'fred']
 
// Create custom iteratee shorthands.
_.iteratee = _.wrap(_.iteratee, function(iteratee, func) {
  return !_.isRegExp(func) ? iteratee(func) : function(string) {
    return func.test(string);
  };
});
 
_.filter(['abc', 'def'], /ef/);
// => ['def']
```

## 生成唯一值

### uniqueId（生成唯一值）

```javascript
_.uniqueId([prefix='']);
```
```javascript
_.uniqueId('contact_');
// => 'contact_104'
 
_.uniqueId();
// => '105'
```

## 设置默认值

### defaultTo（返回值，或默认值）
> 值 ? 值 : 默认值

```javascript
_.defaultTo(value, defaultValue);
```
```javascript
_.defaultTo(1, 10);
// => 1
 
_.defaultTo(undefined, 10);
// => 10
```

## 深匹配

### matches（深度匹配）
> 返回新函数

```javascript
_.matches(source);
````
```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];
 
_.filter(objects, _.matches({ 'a': 4, 'c': 6 }));
// => [{ 'a': 4, 'b': 5, 'c': 6 }]
```

### matchesProperty（路径匹配）

```javascript
_.matchesProperty(path, srcValue)
```
```javascript
var objects = [
  { 'a': 1, 'b': 2, 'c': 3 },
  { 'a': 4, 'b': 5, 'c': 6 }
];
 
_.find(objects, _.matchesProperty('a', 4));
// => { 'a': 4, 'b': 5, 'c': 6 }
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

## 返回参数的函数

### constant（函数，返回传入的首个参数）
> 返回一个函数

```javascript
_.constant(value);
````
```javascript
var objects = _.times(2, _.constant({ 'a': 1 }));
 
console.log(objects);
// => [{ 'a': 1 }, { 'a': 1 }]
 
console.log(objects[0] === objects[1]);
// => true
```

### identity（立刻，返回传入的首个参数）
> 返回结果

```javascript
_.identity(value);
```
```javascript
var object = { 'a': 1 };
 
console.log(_.identity(object) === object);
// => true
```

### nthArg（函数，返回指定位置的函数）

```javascript
_.nthArg([n=0]);
```
```javascript
var func = _.nthArg(1);
func('a', 'b', 'c', 'd');
// => 'b'
 
var func = _.nthArg(-2);
func('a', 'b', 'c', 'd');
// => 'c'
```

## 流函数

### flow（正流函数，上一个是下一个的参数）
> 返回新函数

```javascript
_.flow([funcs]);
```
```javascript
function square(n) {
  return n * n;
}
 
var addSquare = _.flow([_.add, square]);
addSquare(1, 2);
// => 9
```

### flow（反流函数，上一个是下一个的参数）
> 返回新函数

```javascript
_.flowRight([funcs])
```
```javascript
function square(n) {
  return n * n;
}
 
var addSquare = _.flowRight([square, _.add]);
addSquare(1, 2);
// => 9
```

## 同一参数，迭代调用，返回结果

### over（同一参数，批量调用函数）
> 返回新函数

```javascript
_.over([iteratees=[_.identity]])
```
```javascript
var func = _.over([Math.max, Math.min]);
 
func(1, 2, 3, 4);
// => [4, 1]
```

### overEvery（判断是否全都是真值）
> 返回新函数

```javascript
_.overEvery([predicates=[_.identity]]);
```
```javascript
var func = _.overEvery([Boolean, isFinite]);
 
func('1');
// => true
 
func(null);
// => false
 
func(NaN);
// => false
```

### overSome（判断是否有真值存在）
> 返回新函数

```javascript
_.overSome([predicates=[_.identity]]);
```
```javascript
var func = _.overSome([Boolean, isFinite]);
 
func('1');
// => true
 
func(null);
// => true
 
func(NaN);
// => false
```

## 返回给定对象 path 的值函数

### property

```javascript
_.property(path);
```
```javascript
var objects = [
  { 'a': { 'b': 2 } },
  { 'a': { 'b': 1 } }
];
 
_.map(objects, _.property('a.b'));
// => [2, 1]
 
_.map(_.sortBy(objects, _.property(['a', 'b'])), 'a.b');
// => [1, 2]
```

## 返回固定值

### noop（返回 undefined）

```javascript
_.noop();
```
```javascript
_.times(2, _.noop);
// => [undefined, undefined]
```

### stubTrue（返回 true）

```javascript
_.stubTrue();
```
```javascript
_.times(2, _.stubTrue);
// => [true, true]
````

### stubFalse（返回 false）

```javascript
_.stubFalse();
```
```javascript
_.times(2, _.stubFalse);
// => [false, false]
```

### stubArray（返回空数组）

```javascript
_.stubArray();
```
```javascript
var arrays = _.times(2, _.stubArray);
 
console.log(arrays);
// => [[], []]
 
console.log(arrays[0] === arrays[1]);
// => false
```

### stubObject（返回空对象）

```javascript
_.stubObject();
```
```javascript
var objects = _.times(2, _.stubObject);
 
console.log(objects);
// => [{}, {}]
 
console.log(objects[0] === objects[1]);
// => false
```

### stubString（返回空字符串）

```javascript
_.stubString();
```
```javascript
_.times(2, _.stubString);
// => ['', '']
```

## 未整理

### method

```javascript
_.method(path, [args])
```
```javascript
var objects = [
  { 'a': { 'b': _.constant(2) } },
  { 'a': { 'b': _.constant(1) } }
];
 
_.map(objects, _.method('a.b'));
// => [2, 1]
 
_.map(objects, _.method(['a', 'b']));
// => [2, 1]
```

### methodOf

```javascript
_.methodOf(object, [args]);
```
```javascript
var array = _.times(3, _.constant),
    object = { 'a': array, 'b': array, 'c': array };
 
_.map(['a[2]', 'c[0]'], _.methodOf(object));
// => [2, 0]
 
_.map([['a', '2'], ['c', '0']], _.methodOf(object));
// => [2, 0]
```

### mixin

```javascript
_.mixin([object=lodash], source, [options={}]);
```
```javascript
function vowels(string) {
  return _.filter(string, function(v) {
    return /[aeiou]/i.test(v);
  });
}
 
_.mixin({ 'vowels': vowels });
_.vowels('fred');
// => ['e']
 
_('fred').vowels().value();
// => ['e']
 
_.mixin({ 'vowels': vowels }, { 'chain': false });
_('fred').vowels();
// => ['e']
```

### noConflict

```javascript
_.noConflict();
```
```javascript
var lodash = _.noConflict();
```

### propertyOf

```javascript
_.propertyOf(object);
```
```javascript
var array = [0, 1, 2],
    object = { 'a': array, 'b': array, 'c': array };
 
_.map(['a[2]', 'c[0]'], _.propertyOf(object));
// => [2, 0]
 
_.map([['a', '2'], ['c', '0']], _.propertyOf(object));
// => [2, 0]
```

### runInContext

```javascript
_.runInContext([context=root]);
```
```javascript
_.mixin({ 'foo': _.constant('foo') });
 
var lodash = _.runInContext();
lodash.mixin({ 'bar': lodash.constant('bar') });
 
_.isFunction(_.foo);
// => true
_.isFunction(_.bar);
// => false
 
lodash.isFunction(lodash.foo);
// => false
lodash.isFunction(lodash.bar);
// => true
 
// 使用 `context` 模拟 `Date#getTime` 调用 `_.now`
var stubbed = _.runInContext({
  'Date': function() {
    return { 'getTime': stubGetTime };
  }
});
 
// 或者在 Node.js 中创建一个更高级的 `defer`
var defer = _.runInContext({ 'setTimeout': setImmediate }).defer;
```