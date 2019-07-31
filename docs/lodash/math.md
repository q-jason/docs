## 随机数

### random

```javascript
_.random([lower=0], [upper=1], [floating])
```
```javascript
_.random(0, 5);
// => an integer between 0 and 5
 
_.random(5);
// => also an integer between 0 and 5
 
_.random(5, true);
// => a floating-point number between 0 and 5
 
_.random(1.2, 5.2);
// => a floating-point number between 1.2 and 5.2
```

## 上下舍入
> 返回 number <br/>
> precision 为 保留几位小数，该值可以为 负数

### floor（向下舍入）

```javascript
_.floor(number, [precision=0]);
```
```javascript
_.floor(4.006);
// => 4
 
_.floor(0.046, 2);
// => 0.04
 
_.floor(4060, -2);
// => 4000
```

### ceil（向上舍入）

```javascript
_.ceil(number, [precision=0])
```
```javascript
_.ceil(4.006);
// => 5
 
_.ceil(6.004, 2);
// => 6.01
 
_.ceil(6040, -2);
// => 6100
```

### round（四舍五入）

```javascript
_.round(number, [precision=0]);
```
```javascript
_.round(4.006);
// => 4
 
_.round(4.006, 2);
// => 4.01
 
_.round(4060, -2);
// => 4100
```

## 求和

### sum

```javascript
_.sum(array);
```
```javascript
_.sum([4, 2, 8, 6]);
// => 20
```

### sumBy（根据迭代器返回值，求和）

```javascript
_.sumBy(array, [iteratee=_.identity])
```
```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];
 
_.sumBy(objects, function(o) { return o.n; });
// => 20
 
// The `_.property` iteratee shorthand.
_.sumBy(objects, 'n');
// => 20
```

## 选出最大（最小）值

### max（最大值）

```javascript
_.max(array);
```
```javascript
_.max([4, 2, 8, 6]);
// => 8
 
_.max([]);
// => undefined
```

### maxBy（最大值，根据迭代器返回值）

```javascript
_.maxBy(array, [iteratee=_.identity]);
```
```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];
 
_.maxBy(objects, function(o) { return o.n; });
// => { 'n': 2 }
 
// The `_.property` iteratee shorthand.
_.maxBy(objects, 'n');
// => { 'n': 2 }
```

### min（最小值）

```javascript
_.min(array);
```
```javascript
_.min([4, 2, 8, 6]);
// => 2
 
_.min([]);
// => undefined
```

### minBy（最小值，根据迭代器返回值）

```javascript
_.minBy(array, [iteratee=_.identity]);
```
```javascript
var objects = [{ 'n': 1 }, { 'n': 2 }];
 
_.minBy(objects, function(o) { return o.n; });
// => { 'n': 1 }
 
// The `_.property` iteratee shorthand.
_.minBy(objects, 'n');
// => { 'n': 1 }
```

## 计算平均值

### mean

```javascript
_.mean(array);
```
```javascript
_.mean([4, 2, 8, 6]);
// => 5
```

### meanBy（根据迭代器返回值计算）

```javascript
_.meanBy(array, [iteratee=_.identity]);
```
```javascript
var objects = [{ 'n': 4 }, { 'n': 2 }, { 'n': 8 }, { 'n': 6 }];
 
_.meanBy(objects, function(o) { return o.n; });
// => 5
 
// The `_.property` iteratee shorthand.
_.meanBy(objects, 'n');
// => 5
```

## 限制

### clamp（返回限制在 上限 和 下限 之间的值）

```javascript
_.clamp(number, [lower], upper);
```
```javascript
_.clamp(-10, -5, 5);
// => -5
 
_.clamp(10, -5, 5);
// => 5
```

## 范围检查（检查 n 是否在 start 与 end 之间）

### inRange

```javascript
_.inRange(number, [start=0], end);
```
```javascript
_.inRange(3, 2, 4);
// => true
 
_.inRange(4, 8);
// => true
 
_.inRange(4, 2);
// => false
 
_.inRange(2, 2);
// => false
 
_.inRange(1.2, 2);
// => true
 
_.inRange(5.2, 4);
// => false
 
_.inRange(-3, -2, -6);
// => true
```

## 加减乘除

### add（加）

```javascript
_.add(augend, addend);
```
```javascript
_.add(6, 4);
// => 10
```

### subtract（减）

```javascript
_.subtract(minuend, subtrahend)
```
```javascript
_.subtract(6, 4);
// => 2
```

### multiply（乘）

```javascript
_.multiply(multiplier, multiplicand);
```
```javascript
_.multiply(6, 4);
// => 24
```

### divide（除）

```javascript
_.divide(dividend, divisor)
```
```javascript
_.divide(6, 4);
// => 1.5
```

