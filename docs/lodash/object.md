## 合并对象

### assign（替换合并，不包含继承属性）
> 改变目标对象

```javascript
_.assign(object, [sources]);
```
```javascript
function Foo() {
  this.a = 1;
}
 
function Bar() {
  this.c = 3;
}
 
Foo.prototype.b = 2;
Bar.prototype.d = 4;
 
_.assign({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'c': 3 }
```

### merge（合并合并，不包含继承属性）
> 返回目标对象

```javascript
_.merge(object, [sources])
```
```javascript
var object = {
  'a': [{ 'b': 2 }, { 'd': 4 }]
};
 
var other = {
  'a': [{ 'c': 3 }, { 'e': 5 }]
};
 
_.merge(object, other);
// => { 'a': [{ 'b': 2, 'c': 3 }, { 'd': 4, 'e': 5 }] }
```

### assignIn（替换合并，包含继承属性）
> 改变目标对象

```javascript
_.assignIn(object, [sources]);
```
```javascript
function Foo() {
  this.a = 1;
}
 
function Bar() {
  this.c = 3;
}
 
Foo.prototype.b = 2;
Bar.prototype.d = 4;
 
_.assignIn({ 'a': 0 }, new Foo, new Bar);
// => { 'a': 1, 'b': 2, 'c': 3, 'd': 4 }
```

### assignWith（替换合并，合并器返回值）
> 改变目标对象

```javascript
_.assignWith(object, sources, [customizer]);
```
```javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}
 
var defaults = _.partialRight(_.assignWith, customizer);
 
defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### mergeWith（合并合并，合并器返回值）
> 返回目标对象

```javascript
_.mergeWith(object, sources, customizer);
```
```javascript
function customizer(objValue, srcValue) {
  if (_.isArray(objValue)) {
    return objValue.concat(srcValue);
  }
}
 
var object = { 'a': [1], 'b': [2] };
var other = { 'a': [3], 'b': [4] };
 
_.mergeWith(object, other, customizer);
// => { 'a': [1, 3], 'b': [2, 4] }
```

### assignInWith（替换合并，合并器返回值）
> 改变目标对象

```javascript
_.assignInWith(object, sources, [customizer]);
```
```javascript
function customizer(objValue, srcValue) {
  return _.isUndefined(objValue) ? srcValue : objValue;
}
 
var defaults = _.partialRight(_.assignInWith, customizer);
 
defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

------------------------------------------------------------

## 设置默认值

### defaults（给对象设置默认属性值）
> 返回目标对象

```javascript
_.defaults(object, [sources])
```
```javascript
_.defaults({ 'a': 1 }, { 'b': 2 }, { 'a': 3 });
// => { 'a': 1, 'b': 2 }
```

### defaultsDeep（递归设置默认属性值）

```javascript
_.defaultsDeep(object, [sources]);
```
```javascript
_.defaultsDeep({ 'a': { 'b': 2 } }, { 'a': { 'b': 1, 'c': 3 } });
// => { 'a': { 'b': 2, 'c': 3 } }
```

## 获取属性

### get（path，可设置默认值）
> 返回属性值

```javascript
_.get(object, path, [defaultValue]);
```
```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };
 
_.get(object, 'a[0].b.c');
// => 3
 
_.get(object, ['a', '0', 'b', 'c']);
// => 3
 
_.get(object, 'a.b.c', 'default');
// => 'default'
```

## 赋值属性

### set（path，指定值）
> 返回目标对象

```javascript
_.set(object, path, value);
```
```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };
 
_.set(object, 'a[0].b.c', 4);
console.log(object.a[0].b.c);
// => 4
 
_.set(object, ['x', '0', 'y', 'z'], 5);
console.log(object.x[0].y.z);
// => 5
```

### update（path，函数返回值）
> 返回目标对象

```javascript
_.update(object, path, updater);
```
```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }] };
 
_.update(object, 'a[0].b.c', function(n) { return n * n; });
console.log(object.a[0].b.c);
// => 9
 
_.update(object, 'x[0].y.z', function(n) { return n ? n + 1 : 0; });
console.log(object.x[0].y.z);
// => 0
```

### setWith（感觉用处不大）

```javascript
_.setWith(object, path, value, [customizer]);
```
```javascript
var object = {};
 
_.setWith(object, '[0][1]', 'a', Object);
// => { '0': { '1': 'a' } }
```

### updateWith（感觉用处不大）

```javascript
_.updateWith(object, path, updater, [customizer]);
```
```javascript
var object = {};
 
_.updateWith(object, '[0][1]', _.constant('a'), Object);
// => { '0': { '1': 'a' } }
```

## 删除属性

### omit（指定属性，返回新对象）
> 返回新对象

```javascript
_.omit(object, [props])
```
```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.omit(object, ['a', 'c']);
// => { 'b': '2' }
```

### omitBy（通过判断器返回值，删除属性）
> 返回新对象

```javascript
_.omitBy(object, [predicate=_.identity]);
```
```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.omitBy(object, _.isNumber);
// => { 'b': '2' }
```

### unset（指定 key，影响源对象）
> 返回 true 或 false，代表删除成功与否

```javascript
_.unset(object, path);
```
```javascript
var object = { 'a': [{ 'b': { 'c': 7 } }] };
_.unset(object, 'a[0].b.c');
// => true
 
console.log(object);
// => { 'a': [{ 'b': {} }] };
 
_.unset(object, ['a', '0', 'b', 'c']);
// => true
 
console.log(object);
// => { 'a': [{ 'b': {} }] };
```

## 筛选属性
> 返回新对象

### pick（指定属性）
> 返回新对象

```javascript
_.pick(object, [props]);
```
```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.pick(object, ['a', 'c']);
// => { 'a': 1, 'c': 3 }
```

### pickBy（函数返回值指定）
> 返回新对象

```javascript
_.pickBy(object, [predicate=_.identity]);
```
```javascript
var object = { 'a': 1, 'b': '2', 'c': 3 };
 
_.pickBy(object, _.isNumber);
// => { 'a': 1, 'c': 3 }
```

## 提取出所有 key

### keys（不包含继承属性）
> 返回新数组

```javascript
_.keys(object);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.keys(new Foo);
// => ['a', 'b'] (iteration order is not guaranteed)
 
_.keys('hi');
// => ['0', '1']
```

### keysIn（包含继承属性）
> 返回新数组

```javascript
_.keysIn(object);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.keysIn(new Foo);
// => ['a', 'b', 'c'] (iteration order is not guaranteed)
```

## 提取出所有 value

### values（不包含继承属性）
> 返回新数组

```javascript
_.values(object);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.values(new Foo);
// => [1, 2] (无法保证遍历的顺序)
 
_.values('hi');
// => ['h', 'i']
```

### valuesIn（包含继承属性）
> 返回新数组

```javascript
_.valuesIn(object);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.valuesIn(new Foo);
// => [1, 2, 3] (无法保证遍历的顺序)
```

## 批量修改 key

### mapKeys（修改对象 key）
> 返回新对象

```javascript
_.mapKeys(object, [iteratee=_.identity]);
```
```javascript
_.mapKeys({ 'a': 1, 'b': 2 }, function(value, key) {
  return key + value;
});
// => { 'a1': 1, 'b2': 2 }
```

## 批量修改 value

### mapValues（修改对象 value）
> 返回新对象

```javascript
_.mapValues(object, [iteratee=_.identity]);
```
```javascript
var users = {
  'fred':    { 'user': 'fred',    'age': 40 },
  'pebbles': { 'user': 'pebbles', 'age': 1 }
};
 
_.mapValues(users, function(o) { return o.age; });
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
 
// The `_.property` iteratee shorthand.
_.mapValues(users, 'age');
// => { 'fred': 40, 'pebbles': 1 } (iteration order is not guaranteed)
```

## 查找 value，返回 key

### findKey（正向，迭代器，返回 key）
> 返回匹配的 key，否则返回 undefined。

```javascript
_.findKey(object, [predicate=_.identity]);
```
```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};
 
_.findKey(users, function(o) { return o.age < 40; });
// => 'barney' (iteration order is not guaranteed)
 
// The `_.matches` iteratee shorthand.
_.findKey(users, { 'age': 1, 'active': true });
// => 'pebbles'
 
// The `_.matchesProperty` iteratee shorthand.
_.findKey(users, ['active', false]);
// => 'fred'
 
// The `_.property` iteratee shorthand.
_.findKey(users, 'active');
// => 'barney'
```

### findLastKey（反向，迭代器，返回 key）
> 返回匹配的 key，否则返回 undefined。

```javascript
_.findLastKey(object, [predicate=_.identity]);
```
```javascript
var users = {
  'barney':  { 'age': 36, 'active': true },
  'fred':    { 'age': 40, 'active': false },
  'pebbles': { 'age': 1,  'active': true }
};
 
_.findLastKey(users, function(o) { return o.age < 40; });
// => returns 'pebbles' assuming `_.findKey` returns 'barney'
 
// The `_.matches` iteratee shorthand.
_.findLastKey(users, { 'age': 36, 'active': true });
// => 'barney'
 
// The `_.matchesProperty` iteratee shorthand.
_.findLastKey(users, ['active', false]);
// => 'fred'
 
// The `_.property` iteratee shorthand.
_.findLastKey(users, 'active');
// => 'pebbles'
```

## 判断对象是否含有指定属性

### has（path，不包含继承属性）
> 返回 true 或 false

```javascript
_.has(object, path);
```
```javascript
var object = { 'a': { 'b': 2 } };
var other = _.create({ 'a': _.create({ 'b': 2 }) });
 
_.has(object, 'a');
// => true
 
_.has(object, 'a.b');
// => true
 
_.has(object, ['a', 'b']);
// => true
 
_.has(other, 'a');
// => false
```

### hashIn（path，包含继承属性）
> 返回 true 或 false

```javascript
_.hasIn(object, path);
```
```javascript
var object = _.create({ 'a': _.create({ 'b': 2 }) });
 
_.hasIn(object, 'a');
// => true
 
_.hasIn(object, 'a.b');
// => true
 
_.hasIn(object, ['a', 'b']);
// => true
 
_.hasIn(object, 'b');
// => false
```

## 指定多个属性路径，组成数组

### at
> 返回新数组

```javascript
_.at(object, [paths]);
```
```javascript
var object = { 'a': [{ 'b': { 'c': 3 } }, 4] };
 
_.at(object, ['a[0].b.c', 'a[1]']);
// => [3, 4]
```

## 倒置 key 和 value

### invert（相同的 key 会覆盖）
> 返回新对象

```javascript
_.invert(object);
```
```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };
 
_.invert(object);
// => { '1': 'c', '2': 'b' }
```

### invertBy（value 为数组，key 是返回值）
> 返回新数组

```javascript
_.invertBy(object, [iteratee=_.identity]);
```
```javascript
var object = { 'a': 1, 'b': 2, 'c': 1 };
 
_.invertBy(object);
// => { '1': ['a', 'c'], '2': ['b'] }
 
_.invertBy(object, function(value) {
  return 'group' + value;
});
// => { 'group1': ['a', 'c'], 'group2': ['b'] }
```

## 调用对象 path 方法

### invoke
> 返回结果

```javascript
_.invoke(object, path, [args]);
```
```javascript
var object = { 'a': [{ 'b': { 'c': [1, 2, 3, 4] } }] };
 
_.invoke(object, 'a[0].b.c.slice', 1, 3);
// => [2, 3]
```

### result

```javascript
_.result(object, path, [defaultValue]);
```
```javascript
var object = { 'a': [{ 'b': { 'c1': 3, 'c2': _.constant(4) } }] };
 
_.result(object, 'a[0].b.c1');
// => 3
 
_.result(object, 'a[0].b.c2');
// => 4
 
_.result(object, 'a[0].b.c3', 'default');
// => 'default'
 
_.result(object, 'a[0].b.c3', _.constant('default'));
// => 'default'
```

## 遍历

### forIn（正向遍历）

```javascript
_.forIn(object, [iteratee=_.identity]);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.forIn(new Foo, function(value, key) {
  console.log(key);
});
// => Logs 'a', 'b', then 'c' (无法保证遍历的顺序)。
```

### forInRight（反向遍历）

```javascript
_.forInRight(object, [iteratee=_.identity]);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.forInRight(new Foo, function(value, key) {
  console.log(key);
});
// => 输出 'c', 'b', 然后 'a'， `_.forIn` 会输出 'a', 'b', 然后 'c'。
```

### forOwn（正向，不会出现继承属性）

```javascript
_.forOwn(object, [iteratee=_.identity]);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.forOwn(new Foo, function(value, key) {
  console.log(key);
});
// => 输出 'a' 然后 'b' (无法保证遍历的顺序)。
```

### forOwnRight（反向，不会出现继承属性）

```javascript
_.forOwnRight(object, [iteratee=_.identity]);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.forOwnRight(new Foo, function(value, key) {
  console.log(key);
});
// =>  输出 'b' 然后 'a'， `_.forOwn` 会输出 'a' 然后 'b'
```

## 检查对象属性值

### conforms
> 返回一个新的检查函数，调用时传入对象

```javascript
_.conforms(source);
```
```javascript
var objects = [
  { 'a': 2, 'b': 1 },
  { 'a': 1, 'b': 2 }
];
 
_.filter(objects, _.conforms({ 'b': function(n) { return n > 1; } }));
// => [{ 'a': 1, 'b': 2 }]
```

### conformsTo
> 区别于 conforms，该函数立刻执行，返回 true 或 false

```javascript
_.conformsTo(object, source);
```
```javascript
var object = { 'a': 1, 'b': 2 };

_.conformsTo(object, { 'b': function(n) { return n > 1; } });
// => true
_.conformsTo(object, { 'b': function(n) { return n > 2; } });
// => false
```

## 统计出类型是 Function 的属性名，组成数组

### functions（不包含继承属性）
> 返回新数组

```javascript
_.functions(object);
```
```javascript
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}
 
Foo.prototype.c = _.constant('c');
 
_.functions(new Foo);
// => ['a', 'b']
```

### functionsIn（包含继承属性）
> 返回新数组

```javascript
_.functionsIn(object);
```
```javascript
function Foo() {
  this.a = _.constant('a');
  this.b = _.constant('b');
}
 
Foo.prototype.c = _.constant('c');
 
_.functionsIn(new Foo);
// => ['a', 'b', 'c']
```

## 原型操作

### create

```javascript
_.create(prototype, [properties]);
```
```javascript
function Shape() {
  this.x = 0;
  this.y = 0;
}
 
function Circle() {
  Shape.call(this);
}
 
Circle.prototype = _.create(Shape.prototype, {
  'constructor': Circle
});
 
var circle = new Circle;
console.log(circle instanceof Circle);
// => true
 
console.log(circle instanceof Shape);
// => true
```

## 将对象拆分成二维数组
> 返回新的二维数组，_.fromPairs反向版

### toPairs（不包含继承属性）

```javascript
_.toPairs(object);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.toPairs(new Foo);
// => [['a', 1], ['b', 2]] (iteration order is not guaranteed)
```

### toPairs（包含继承属性）

```javascript
_.toPairsIn(object);
```
```javascript
function Foo() {
  this.a = 1;
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.toPairsIn(new Foo);
// => [['a', 1], ['b', 2], ['c', 3]] (iteration order is not guaranteed)
```

## 迭代累加转换
> 其实和 _.reduce 一毛一样

### transform
> 返回叠加后的值

```javascript
_.transform(object, [iteratee=_.identity], [accumulator]);
```
```javascript
_.transform([2, 3, 4], function(result, n) {
  result.push(n *= n);
  return n % 2 === 0;
}, []);
// => [4, 9]
 
_.transform({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
}, {});
// => { '1': ['a', 'c'], '2': ['b'] }
```