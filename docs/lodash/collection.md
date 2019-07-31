## 获取指定元素

### nth（指定下标）

```javascript
// 获取数组中指定下标的元素
_.nth(array, [n=0]);
```
```javascript
_.nth(['a', 'b', 'c', 'd'], 1);
// => 'b'
```

### head/first（第一个元素）

```javascript
// 获取数组的第一个元素
_.head(array);
_.first(array);
```

```javascript
_.head([1, 2, 3]);
// => 1

// 获取数组的第一个元素
_.first([1, 2, 3]);
// => 1
```

### last（最后一个元素）

```javascript
// 获取数组的最后一个元素
_.last(array);
```

```javascript
_.last([1, 2, 3]);
// => 3
```

### find（迭代器，正向匹配）

```javascript
// 正向遍历
// 返回迭代器第一个返回 true 的元素
_.find(collection, [predicate=_.identity], [fromIndex=0]);
```
```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];
 
_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'
 
// The `_.matches` iteratee shorthand.
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'
 
// The `_.matchesProperty` iteratee shorthand.
_.find(users, ['active', false]);
// => object for 'fred'
 
// The `_.property` iteratee shorthand.
_.find(users, 'active');
// => object for 'barney'
```

### findLast（迭代器，反向匹配）

```javascript
// 反向遍历
// 返回迭代器第一个返回 true 的元素
_.findLast(collection, [predicate=_.identity], [fromIndex=collection.length-1]);
```
```javascript
_.findLast([1, 2, 3, 4], function(n) {
  return n % 2 === 1;
});
// => 3
```

## 范围选择元素

### slice（下标区域选择）

```javascript
// 选取从 start 到 end 的元素
// 注意：不包括 end
_.slice(array, [start=0], [end=array.length])
```
```javascript
_.slice([1, 2, 3, 4], 0, 3);
// => [1, 2, 3];
```

### tail（第一个元素外的所有元素）

```javascript
// 选取数组第一个元素之外
// 所有其他元素
_.tail(array);
```
```javascript
_.tail([1, 2, 3]);
// => [2, 3]
```

### initial（最后一个元素外的所有元素）

```javascript
// 选择数组最后一个元素之外
// 所有其他元素
_.initial(array);
```
```javascript
_.initial([1, 2, 3]);
// => [1, 2]
```

### take（开头或结尾的 n 个元素）

```javascript
// 选取数组开头的 n 个元素
_.take(array, [n=1]);

// 选取数组结尾的 n 个元素
_.takeRight(array, [n=1]);

// 通过迭代器
// 从开头选择元素
// 直到迭代器返回 false
_.takeWhile(array, [predicate=_.identity]);

// 通过迭代器
// 从结尾选择元素
// 直到迭代器返回 false
_.takeRightWhile(array, [predicate=_.identity]);
```
```javascript
_.take([1, 2, 3], 2);
// => [1, 2]

_.takeRight([1, 2, 3], 2);
// => [2, 3]

_.takeWhile([1, 2, 3, 4, 5, 6], num => num < 4);
// => [1, 2, 3]

_.takeRightWhile([1, 2, 3, 4, 5, 6], num => num > 4);
// => [5, 6]
```

### drop（头或尾元素之外的其余元素）

```javascript
// 选取去掉开头的前 n 个元素之外的所有其他元素
_.drop(array, [n=1]);

// 返回去掉结尾的 n 个元素之外的所有其他元素
_.dropRight(array, [n=1]);

// 从开头到结尾循环删除，直到返回 false 为止，返回剩下的元素
_.dropWhile(array, [predicate=_.identity]);

// 从结尾到开头循环删除，直到返回 false 为止，返回剩下的元素
_.dropRightWhile(array, [predicate=_.identity]);
```
```javascript
_.drop([1, 2, 3], 2);
// => [3]

_.dropRight([1, 2, 3], 2);
// => [1]

_.dropWhile([ 1, 2, 3 ], num => num < 3);
// => [3]

_.dropRightWhile([ 1, 2, 3 ], num => num > 1);
// => [1]
```

## 寻找元素下标

### indexOf（全等匹配）

```javascript
// 从前向后
// 全等比较
// 返回下标
// 没找到会返回 -1
_.indexOf(array, value, [fromIndex=0]);

// 从后向前
// 全等比较
// 返回下标
// 没找到会返回 -1
_.lastIndexOf(array, value, [fromIndex=array.length-1]);
```
```javascript
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3

_.lastIndexOf([1, 2, 1, 2], 2);
// => 3
```

### findIndex（迭代器匹配）

```javascript
// 从前向后
// 通过判断器判断是否相等
// 返回为 true 时的下标
_.findIndex(array, [predicate=_.identity], [fromIndex=0]);

// 从后向前
// 通过判断器判断是否相等
// 返回为 true 时的下标
_.findLastIndex(array, [predicate=_.identity], [fromIndex=array.length-1]);
```
```javascript
_.findIndex([ 1, 2, 3, 4, 5 ], num => num === 5);
// => 4

_.findLastIndex([ 1, 2, 3, 4, 5 ], num => num === 5);
// => 4
```

### sortedIndexOf（没理解啥意思）

```javascript
// 没理解啥意思........
// 这个方法类似 _.indexOf，除了它是在已经排序的数组array上执行二进制检索。
_.sortedIndexOf(array, value);

// 没理解啥意思........
_.sortedLastIndexOf(array, value);
```

## 删除元素

### without（传入指定元素，返回新数组）

```javascript
_.without(array, [values]);
```
```javascript
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

### difference（传入数组, 返回新数组）

```javascript
// 删除数组中指定的元素，全等比较
_.difference(array, [ values ]);

// 通过迭代器将元素进行转换后（返回值）再进行比较
// 返回元素转化前的新数组
_.differenceBy(array, [values], [iteratee=_.identity]);

// 根据判断器的返回值（true 或 false），判断是否相等
_.differenceWith(array, [values], [comparator]);
```
```javascript
_.difference([ 3, 2, 1 ], [ 4, 2 ]);
// => [ 3, 1 ]

_.differenceBy([ 3.1, 2.2, 1.3 ], [ 4.4, 2.5 ], Math.floor);
// => [ 3.1, 1.3 ]

_.differenceBy([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], 'x');
// => [{ 'x': 2 }]

_.differenceWith(
  [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }],
  [{ 'x': 1, 'y': 2 }],
  _.isEqual
);
// => [{ 'x': 2, 'y': 1 }]
```

### pull（传入无限制，影响源数组）

```javascript
// 指定元素
// 全等比较删除
// 返回源数组
_.pull(array, [values]);

// 指定元素数组
// 全等比较删除
// 返回源数组
_.pullAll(array, values);

// 将元素通过迭代器转换
// 将转换后的值进行比较
// 返回源数组（数组中元素为转换前的值）
_.pullAllBy(array, values, [iteratee=_.identity]);

// 根据判断器进行比较
// 根据返回值 true 或 false
// 判断两值是否相等
// 返回源数组
_.pullAllWith(array, values, [comparator]);

// 根据索引移出相应元素
// 返回删除的元素组成的数组
_.pullAt(array, [indexes]);
```
```javascript
_.pull([1, 2, 3, 1, 2, 3], 2, 3);
// => [1, 1]

_.pullAll([1, 2, 3, 1, 2, 3], [2, 3]);
// => [1, 1]

_.pullAllBy([{ 'x': 1 }, { 'x': 2 }, { 'x': 3 }, { 'x': 1 }], [{ 'x': 1 }, { 'x': 3 }], 'x');
// => [{ 'x': 2 }]

_.pullAllWith(
  [{ 'x': 1, 'y': 2 }, { 'x': 3, 'y': 4 }, { 'x': 5, 'y': 6 }],
  [{ 'x': 3, 'y': 4 }],
  _.isEqual
);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]

var array = [5, 10, 15, 20];
var evens = _.pullAt(array, 1, 3);
 
console.log(array);
// => [5, 15]
 
console.log(evens);
// => [10, 20]
```

### remove（传入判断器，影响源数组）

```javascript
_.remove(array, [predicate=_.identity]);
```
```javascript
var array = [1, 2, 3, 4];
var evens = _.remove(array, function(n) {
  return n % 2 === 0;
});
 
console.log(array);
// => [1, 3]
 
console.log(evens);
// => [2, 4]
```

## 判断

### includes（全等判断，某元素是否存在）

```javascript
// 如果指定 fromIndex 是负数，那么从 collection(集合) 的结尾开始检索
// 返回 true 或 false
_.includes(collection, value, [fromIndex=0]);
```
```javascript
_.includes([1, 2, 3], 1);
// => true
 
_.includes([1, 2, 3], 1, 2);
// => false
 
_.includes({ 'user': 'fred', 'age': 40 }, 'fred');
// => true
 
_.includes('pebbles', 'eb');
// => true
````

### some（判断器判断，某元素是否存在）
> 返回 true 或 false

```javascript
// 若判断器返回了 true
// 会立刻停止遍历
// 返回结果
_.some(collection, [predicate=_.identity])
```
```javascript
_.some([null, 0, 'yes', false], Boolean);
// => true
 
var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];
 
// The `_.matches` iteratee shorthand.
_.some(users, { 'user': 'barney', 'active': false });
// => false
 
// The `_.matchesProperty` iteratee shorthand.
_.some(users, ['active', false]);
// => true
 
// The `_.property` iteratee shorthand.
_.some(users, 'active');
// => true
```

### every（是否是全真集合）

```javascript
// 通过迭代器判断数组中是否全都为真
// 返回 true 或 false
_.every(collection, [predicate=_.identity]);
```
```javascript
_.every([true, 1, null, 'yes'], Boolean);
// => false

var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': false }
];
 
// The `_.matches` iteratee shorthand.
_.every(users, { 'user': 'barney', 'active': false });
// => false
 
// The `_.matchesProperty` iteratee shorthand.
_.every(users, ['active', false]);
// => true
 
// The `_.property` iteratee shorthand.
_.every(users, 'active');
// => false
```

## 筛选

### filter（真元素集合）

```javascript
// 遍历数组
// 根据迭代器的返回值
// 筛选出为 true 的元素
// 返回新数组
_.filter(collection, [predicate=_.identity]);
```
```javascript

var users = [
  { 'user': 'barney', 'age': 36, 'active': true },
  { 'user': 'fred',   'age': 40, 'active': false }
];
 
_.filter(users, function(o) { return !o.active; });
// => objects for ['fred']
 
// The `_.matches` iteratee shorthand.
_.filter(users, { 'age': 36, 'active': true });
// => objects for ['barney']
 
// The `_.matchesProperty` iteratee shorthand.
_.filter(users, ['active', false]);
// => objects for ['fred']
 
// The `_.property` iteratee shorthand.
_.filter(users, 'active');
// => objects for ['barney']
```

### reject（假元素集合）
> 返回新数组

```javascript
// 遍历数组
// 通过迭代器的返回值
// 筛选出为假值的集合
// 返回新数组
_.reject(collection, [predicate=_.identity])
```
```javascript
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];
 
_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
 
// `_.matches` 迭代简写
_.reject(users, { 'age': 40, 'active': true });
// => objects for ['barney']
 
// `_.matchesProperty` 迭代简写
_.reject(users, ['active', false]);
// => objects for ['fred']
 
// `_.property` 迭代简写
_.reject(users, 'active');
// => objects for ['barney']
```

### partition（真假元素集合）
> 返回新数组

```javascript
// 将集合按照迭代器的返回值分为 ['真', '假'] 两个数组
// 返回新数组
_.partition(collection, [predicate=_.identity]);
```
```javascript
var users = [
  { 'user': 'barney',  'age': 36, 'active': false },
  { 'user': 'fred',    'age': 40, 'active': true },
  { 'user': 'pebbles', 'age': 1,  'active': false }
];
 
_.partition(users, function(o) { return o.active; });
// => objects for [['fred'], ['barney', 'pebbles']]
 
// The `_.matches` iteratee shorthand.
_.partition(users, { 'age': 1, 'active': false });
// => objects for [['pebbles'], ['barney', 'fred']]
 
// The `_.matchesProperty` iteratee shorthand.
_.partition(users, ['active', false]);
// => objects for [['barney', 'pebbles'], ['fred']]
 
// The `_.property` iteratee shorthand.
_.partition(users, 'active');
// => objects for [['fred'], ['barney', 'pebbles']]
```

## 排序

### sortBy（迭代器，升序排序）
> 返回新数组

```javascript
_.sortBy(collection, [iteratees=[_.identity]])
```
```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 34 }
];
 
_.sortBy(users, function(o) { return o.user; });
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
 
_.sortBy(users, ['user', 'age']);
// => objects for [['barney', 34], ['barney', 36], ['fred', 40], ['fred', 48]]
 
_.sortBy(users, 'user', function(o) {
  return Math.floor(o.age / 10);
});
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

### orderBy（迭代器，多次排序）
> 返回新数组

```javascript
// 通常用于对象集合排序
// 可指定多个属性排序（asc，desc）
// 返回新数组
_.orderBy(collection, [iteratees=[_.identity]], [orders]);
```
```javascript
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 34 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 36 }
];
 
// 以 `user` 升序排序 再  `age` 以降序排序。
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
```

## 合并

### concat（拼接）

```javascript
// 和 Array.prototype.concat 一样
_.concat(array, [values]);
```
```javascript
_.concat([1], 2, [3], [[4]]);
// => [1, 2, 3, [4]]
```

### union（合并，去重）

```javascript
// 返回新数组
_.union([arrays]);

// 先将元素通过迭代器转换
// 合并，去重
// 返回新数组，元素为转换前
_.unionBy([arrays], [iteratee=_.identity]);

// 根据判断器判断两值是否相等
// 合并，去重
// 返回新数组
_.unionWith([arrays], [comparator]);
```
```javascript
_.union([2], [1, 2]);
// => [2, 1]

_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]

// 对象数组可简写
_.unionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]

var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];
 
_.unionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

### intersection（筛选交集，去重）

```javascript
// 筛选出传入的数组中都包含的元素
// 返回新数组
_.intersection([arrays]);

// 先将元素通过迭代器转换
// 再筛选出转换后的值的交集
// 返回新数组
_.intersectionBy([arrays], [iteratee=_.identity]);

// 通过判断器，判断两值是否相等
// 筛选交集
// 返回新数组
_.intersectionWith([arrays], [comparator]);
```
```javascript
_.intersection([2, 1], [4, 2], [1, 2]);
// => [2]

_.intersectionBy([2.1, 1.2], [4.3, 2.4], Math.floor);
// => [2.1]

_.intersectionBy([{ 'x': 1 }], [{ 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }]


var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];
 
_.intersectionWith(objects, others, _.isEqual);
// => [{ 'x': 1, 'y': 2 }]
```

### xor（筛选唯一，去重）

```javascript
// 筛选出传入的多个数组中，唯一的元素
// 返回新数组
_.xor([arrays]);

// 先将元素通过迭代器转换
// 再筛选出多个数组中的唯一值
// 返回新数组，元素为转换前的
_.xorBy([arrays], [iteratee=_.identity]);

// 根据判断器，判断两值是否相等
// 筛选出多个数组中，唯一存在的值
// 返回新数组 
_.xorWith([arrays], [comparator]);
```
```javascript
_.xor([2, 1, 1, 1, 1], [2, 3]);
// => [1, 3]

_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// => [1.2, 3.4]

var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
var others = [{ 'x': 1, 'y': 1 }, { 'x': 1, 'y': 2 }];

_.xorWith(objects, others, _.isEqual);
// => [{ 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

## 去重

### uniq

```javascript
// 全等去重
_.uniq(array);

// 先将值通过迭代器转换
// 比较转换后的值去重
// 返回新数组
_.uniqBy(array, [iteratee=_.identity]);

// 通过判断器，判断两值是否相等
// 进行去重
// 返回新数组
_.uniqWith(array, [comparator]);
```
```javascript
_.uniq([2, 1, 2]);
// => [2, 1]

_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// => [2.1, 1.2]

_.uniqBy([{ 'x': 1 }, { 'x': 2 }, { 'x': 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]

_.uniqWith(
  [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 2 }],
  _.isEqual
);
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }]
```

## 去假值

### compact（数组去假值）

```javascript
// 去除数组中的假值
// false, null, 0, "", undefined, 和 NaN 都是被认为是假值
// 返回新数组
_.compact(array);
```
```javascript
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

## 随机

### sample（随机获取一个元素）
> 返回元素

```javascript
_.sample(collection);
```
```javascript
_.sample([1, 2, 3, 4]);
// => 2
```

### sampleSize（随机获取 n 个元素）
> 返回新数组

```javascript
_.sampleSize(collection, [n=1])
```
```javascript
_.sampleSize([1, 2, 3], 2);
// => [3, 1]
 
_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

### shuffle（打乱数组）
> 返回新数组

```javascript
_.shuffle(collection)
```
```javascript
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2]
```

## 求和

### reduce（正向）
> 返回结果

```javascript
// 遍历集合
// 通过迭代器累加值
// 最终返回结果
_.reduce(collection, [iteratee=_.identity], [accumulator])
```
```javascript
_.reduce([1, 2], function(sum, n) {
  return sum + n;
}, 0);
// => 3
 
_.reduce({ 'a': 1, 'b': 2, 'c': 1 }, function(result, value, key) {
  (result[value] || (result[value] = [])).push(key);
  return result;
}, {});
// => { '1': ['a', 'c'], '2': ['b'] } (无法保证遍历的顺序)
```

### reduceRight（反向）
> 返回结果

```javascript
// 同 reduce
// 不过遍历顺序是反向的
_.reduceRight(collection, [iteratee=_.identity], [accumulator])
```
```javascript
var array = [[0, 1], [2, 3], [4, 5]];
 
_.reduceRight(array, function(flattened, other) {
  return flattened.concat(other);
}, []);
// => [4, 5, 2, 3, 0, 1]
```

## 分组

### groupBy（返回新对象）

```javascript
// 按照迭代器的返回值进行分组
// 返回新对象
_.groupBy(collection, [iteratee=_.identity]);
```
```javascript
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }

// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

### chunk（数组分块）

```javascript
// 按照 size 将数组分成若干小小组
// 返回新的二维数组
_.chunk(array, [size=1]);
```
```javascript
_.chunk(['a', 'b', 'c', 'd'], 3);
// => [['a', 'b', 'c'], ['d']]
```

## 遍历
> 迭代函数中只要返回了 false 就会立刻停止循环

### each（正向遍历）

```javascript
_.each(collection, [iteratee=_.identity]);
_.forEach(collection, [iteratee=_.identity]);
```
```javascript
_([1, 2]).each(function(value) {
  console.log(value);
});
// => Logs `1` then `2`.
```

### eachRight（反向遍历）

```javascript
_.eachRight(collection, [iteratee=_.identity]);
_.forEachRight(collection, [iteratee=_.identity]);
```
```javascript
_.forEachRight([1, 2], function(value) {
  console.log(value);
});
// => Logs `2` then `1`.
```

## 遍历，返回结果

### map
> 返回新数组

```javascript
// 通过迭代器处理值
// 并返回结果，组成新数组
// 返回新数组
_.map(collection, [iteratee=_.identity]);
```
```javascript
function square(n) {
  return n * n;
}
 
_.map([4, 8], square);
// => [16, 64]
 
_.map({ 'a': 4, 'b': 8 }, square);
// => [16, 64] (iteration order is not guaranteed)
 
var users = [
  { 'user': 'barney' },
  { 'user': 'fred' }
];
 
// The `_.property` iteratee shorthand.
_.map(users, 'user');
// => ['barney', 'fred']
```

### invokeMap（和 map 差不多）
> 返回新数组

```javascript
_.invokeMap(collection, path, [args]);
```
```javascript
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort');
// => [[1, 5, 7], [1, 2, 3]]
 
_.invokeMap([123, 456], String.prototype.split, '');
// => [['1', '2', '3'], ['4', '5', '6']]
```

## 填充数组

### fill（用字符填充数组，改变源数组）

```javascript
// 用指定字符串填充指定区域
// 注意 end 不包含
// 改变源数组
_.fill(array, value, [start=0], [end=array.length]);
```
```javascript
_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```

## 降维

### flatten（数组降维）

```javascript
// 降一级
// 返回新数组
_.flatten(array);

// 递归降维，将为一维数组
// 返回新数组
_.flattenDeep(array);

// 指定降多少级
// 返回新数组
_.flattenDepth(array, [depth=1]);
```
```javascript
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]

_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]

_.flattenDepth([1, [2, [3, [4]], 5]], 2);
// => [1, 2, 3, [4], 5]
```

## 数组转对象

### keyBy（迭代器返回值为 key）
> 返回新对象

```javascript
// 根据迭代器的返回值当做 key
// value 为返回 key 的最后一个元素
// 组成新对象
_.keyBy(collection, [iteratee=_.identity]);
```
```javascript
var array = [
  { 'dir': 'left', 'code': 97 },
  { 'dir': 'right', 'code': 100 }
];
 
_.keyBy(array, function(o) {
  return String.fromCharCode(o.code);
});
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }
 
_.keyBy(array, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }
```

### fromPairs（二维数组转为对象）

```javascript
// 二维数组转为对象
// 返回新对象
_.fromPairs(pairs);
```
```javascript
_.fromPairs([['fred', 30], ['barney', 40]]);
// => { 'fred': 30, 'barney': 40 }
```

## 拼接字符串

### join

```javascript
// 同 Array.prototype.join
_.join(array, [separator=',']);
```
```javascript
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'
```

## 翻转

### reverse（数组翻转）

```javascript
// 会改变源数组
_.reverse([1, 2, 3]);
// => [3, 2, 1]
```

## 插入位置计算

### sortedIndex

```javascript
// 计算 value 在 array 中
// 尽可能小的排序位置
// 返回下标
_.sortedIndex(array, value);

// 计算 value 在 array 中
// 尽可能大的排序位置
// 返回下标
_.sortedLastIndex(array, value);

// 根据迭代器的返回值计算尽可能小的位置
// 通常用于对象简写
// 返回位置
_.sortedIndexBy(array, value, [iteratee=_.identity]);

// 根据迭代器的返回值计算尽可能大的位置
// 通常用于对象简写
// 返回位置
_.sortedLastIndexBy(array, value, [iteratee=_.identity]);
```
```javascript
_.sortedIndex([30, 50], 40);
// => 1

_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4

_.sortedIndexBy(
  [{ 'x': 4 }, { 'x': 5 }],
  { 'x': 4 },
  'x'
);
// => 0

_.sortedLastIndexBy(
  [{ 'x': 4 }, { 'x': 5 }],
  { 'x': 4 },
  'x'
);
// => 1
```

## 数组组合

### zip

```javascript
// 将传入的多个数组
// 按照下标组合
// 返回二维数组
_.zip([arrays]);

// 将传入的多个数组，按照迭代器进行组合
_.zipWith([arrays], [iteratee=_.identity]);

// 第一个参数为 key 数组，第二位数组为 value 数组，组合成一个对象
_.zipObject([props=[]], [values=[]]);

// 类似于 zipObject，可以指定 path
_.zipObjectDeep([props=[]], [values=[]]);

// _.zip 的方向版，将二位数组拆分成多个数组
_.unzip(zipped);

// 通过迭代器拆分
_.unzipWith(array, [iteratee=_.identity]);
```
```javascript
_.zip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 30, true], ['barney', 40, false]]

_.zipWith([1, 2], [10, 20], [100, 200], function(a, b, c) {
  return a + b + c;
});
// => [111, 222]

_.zipObject(['a', 'b'], [1, 2]);
// => { 'a': 1, 'b': 2 }

_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { 'a': { 'b': [{ 'c': 1 }, { 'd': 2 }] } }

_.unzip(['fred', 'barney'], [30, 40], [true, false]);
// => [['fred', 'barney'], [30, 40], [true, false]]

_.unzipWith([[1, 10, 100], [2, 20, 200]], _.add);
// => [3, 30, 300]
```

## 统计次数

### countBy（统计次数）

```javascript
// 将迭代器的返回值作为 key，value 为 key 返回的次数
// 返回新对象
_.countBy(collection, [iteratee=_.identity]);
```
```javascript
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }
```

## 创建扁平化数组

### flatMap

```javascript
// 迭代器返回的值都会默认降维一级
// 返回新数组
_.flatMap(collection, [iteratee=_.identity]);

// 递归降维
// 返回新数组
_.flatMapDeep(collection, [iteratee=_.identity]);

// 指定降维级数
// 返回新数组
_.flatMapDepth(collection, [iteratee=_.identity], [depth=1]);
```
```javascript
_.flatMap([1, 2], function (n) {
  return [n, n];
});
// => [1, 1, 2, 2]

_.flatMapDeep([1, 2], function (n) {
  return [[[n, n]]];
});
// => [1, 1, 2, 2]

_.flatMapDepth([1, 2], function (n) {
  return [[[n, n]]];
}, 2);
// => [[1, 1], [2, 2]]
```

## 创建范围数组

### range（正序，从 start 到 end 的数组）
> 返回新数组

```javascript
_.range([start=0], end, [step=1]);
```
```javascript
_.range(4);
// => [0, 1, 2, 3]
 
_.range(-4);
// => [0, -1, -2, -3]
 
_.range(1, 5);
// => [1, 2, 3, 4]
 
_.range(0, 20, 5);
// => [0, 5, 10, 15]
 
_.range(0, -4, -1);
// => [0, -1, -2, -3]
 
_.range(1, 4, 0);
// => [1, 1, 1]
 
_.range(0);
// => []
```

### rangeRight（降序，从 end 到 start 的数组）

```javascript
_.rangeRight([start=0], end, [step=1]);
```
```javascript
_.rangeRight(4);
// => [3, 2, 1, 0]
 
_.rangeRight(-4);
// => [-3, -2, -1, 0]
 
_.rangeRight(1, 5);
// => [4, 3, 2, 1]
 
_.rangeRight(0, 20, 5);
// => [15, 10, 5, 0]
 
_.rangeRight(0, -4, -1);
// => [-3, -2, -1, 0]
 
_.rangeRight(1, 4, 0);
// => [1, 1, 1]
 
_.rangeRight(0);
// => []
```

## 长度

### size
> 如果集合是类数组或字符串，返回其 length 
> 如果集合是对象，返回其可枚举属性的个数。

```javascript
_.size(collection);
```
```javascript
_.size([1, 2, 3]);
// => 3
 
_.size({ 'a': 1, 'b': 2 });
// => 2
 
_.size('pebbles');
// => 7
```