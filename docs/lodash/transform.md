## 克隆

### clone（浅拷贝）
> 返回克隆值

```javascript
_.clone(value);
```
```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var shallow = _.clone(objects);
console.log(shallow[0] === objects[0]);
// => true
```

### cloneDeep（深拷贝）
> 返回克隆值

```javascript
_.cloneDeep(value);
```
```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
// => false
```

### cloneWith（定制克隆值）
> 返回克隆值

```javascript
_.cloneWith(value, [customizer]);
```
```javascript
function customizer(value) {
  if (_.isElement(value)) {
    return value.cloneNode(false);
  }
}
 
var el = _.cloneWith(document.body, customizer);
 
console.log(el === document.body);
// => false
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 0
```

### cloneDeepWith（递归定制克隆值）
> 返回克隆值

```javascript
_.cloneDeepWith(value, [customizer]);
```
```javascript
function customizer(value) {
  if (_.isElement(value)) {
    return value.cloneNode(true);
  }
}
 
var el = _.cloneDeepWith(document.body, customizer);
 
console.log(el === document.body);
// => false
console.log(el.nodeName);
// => 'BODY'
console.log(el.childNodes.length);
// => 20
```

## 转为数组

### toArray（会根据不同类型进行处理）
> 返回新数组

```javascript
_.toArray(value)
```
```javascript
_.toArray({ 'a': 1, 'b': 2 });
// => [1, 2]
 
_.toArray('abc');
// => ['a', 'b', 'c']
 
_.toArray(1);
// => []
 
_.toArray(null);
// => []
```

### castArray（简单粗暴，强制转为数组）
> 返回新数组

```javascript
_.castArray(value);
```
```javascript
_.castArray(1);
// => [1]
 
_.castArray({ 'a': 1 });
// => [{ 'a': 1 }]
 
_.castArray('abc');
// => ['abc']
 
_.castArray(null);
// => [null]
 
_.castArray(undefined);
// => [undefined]
 
_.castArray();
// => []
 
var array = [1, 2, 3];
console.log(_.castArray(array) === array);
// => true
```

### toPath（将 string value 转化为 path 数组）
> 返回新数组

```javascript
_.toPath(value);
```
```javascript
_.toPath('a.b.c');
// => ['a', 'b', 'c']
 
_.toPath('a[0].b.c');
// => ['a', '0', 'b', 'c']
```

## 转为字符串

### toString（会根据不同类型进行处理）

```javascript
_.toString(value);
```
```javascript
_.toString(null);
// => ''
 
_.toString(-0);
// => '-0'
 
_.toString([1, 2, 3]);
// => '1,2,3'
```

## 转为数字

### toNumber（转为数字）

```javascript
_.toNumber(value)
```
```javascript
_.toNumber(3.2);
// => 3.2
 
_.toNumber(Number.MIN_VALUE);
// => 5e-324
 
_.toNumber(Infinity);
// => Infinity
 
_.toNumber('3.2');
// => 3.2
```

### parseInt（转为整数，同 ES5 parseInt）

```javascript
_.parseInt(string, [radix=10])
```
```javascript
_.parseInt('08');
// => 8
 
_.map(['6', '08', '10'], _.parseInt);
// => [6, 8, 10]
```

### toSafeInteger（转为安全数字）

```javascript
_.toSafeInteger(value);
```
```javascript
_.toSafeInteger(3.2);
// => 3
 
_.toSafeInteger(Number.MIN_VALUE);
// => 0
 
_.toSafeInteger(Infinity);
// => 9007199254740991
 
_.toSafeInteger('3.2');
// => 3
```

### toFinite（转为有限数字）

```javascript
_.toFinite(value)
```
```javascript
_.toFinite(3.2);
// => 3.2
 
_.toFinite(Number.MIN_VALUE);
// => 5e-324
 
_.toFinite(Infinity);
// => 1.7976931348623157e+308
 
_.toFinite('3.2');
// => 3.2
```

### toInteger（转为整数，舍弃小数位）

```javascript
_.toInteger(value)
```
```javascript
_.toInteger(3.2);
// => 3
 
_.toInteger(Number.MIN_VALUE);
// => 0
 
_.toInteger(Infinity);
// => 1.7976931348623157e+308
 
_.toInteger('3.2');
// => 3
```

### toLength（转为有效 length，舍弃小数位）

```javascript
_.toLength(value)
```
```javascript
_.toLength(3.2);
// => 3
 
_.toLength(Number.MIN_VALUE);
// => 0
 
_.toLength(Infinity);
// => 4294967295
 
_.toLength('3.2');
// => 3
```

## 转为对象

### toPlainObject（包括继承的可枚举属性）

```javascript
_.toPlainObject(value);
```
```javascript
function Foo() {
  this.b = 2;
}
 
Foo.prototype.c = 3;
 
_.assign({ 'a': 1 }, new Foo);
// => { 'a': 1, 'b': 2 }
 
_.assign({ 'a': 1 }, _.toPlainObject(new Foo));
// => { 'a': 1, 'b': 2, 'c': 3 }
```
