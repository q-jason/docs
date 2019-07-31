## 是否 相等

### eq（全等，浅比较）

```javascript
_.eq(value, other);
```
```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };
 
_.eq(object, object);
// => true
 
_.eq(object, other);
// => false
 
_.eq('a', 'a');
// => true
 
_.eq('a', Object('a'));
// => false
 
_.eq(NaN, NaN);
// => true
```

### isEqual（全等，深比较）

```javascript
_.isEqual(value, other)
```
```javascript
var object = { 'a': 1 };
var other = { 'a': 1 };
 
_.isEqual(object, other);
// => true
 
console.log(object === other);
// => false
```

### isEqualWith（全等，自定义比较器）

```javascript
_.isEqualWith(value, other, [customizer]);
```
```javascript
function isGreeting(value) {
  return /^h(?:i|ello)$/.test(value);
}
 
function customizer(objValue, othValue) {
  if (isGreeting(objValue) && isGreeting(othValue)) {
    return true;
  }
}
 
var array = ['hello', 'goodbye'];
var other = ['hi', 'goodbye'];
 
_.isEqualWith(array, other, customizer);
// => true
```

## 是否 匹配

### isMatch（深比较，是否匹配）

```javascript
_.isMatch(object, source);
```
```javascript
var object = { 'a': 1, 'b': 2 };
 
_.isMatch(object, { 'b': 2 });
// => true
 
_.isMatch(object, { 'b': 1 });
// => false
```

### isMatchWith（深比较，自定义比较函数）

```javascript
_.isMatchWith(object, source, [customizer]);
```
```javascript
function isGreeting(value) {
  return /^h(?:i|ello)$/.test(value);
}
 
function customizer(objValue, srcValue) {
  if (isGreeting(objValue) && isGreeting(srcValue)) {
    return true;
  }
}
 
var object = { 'greeting': 'hello' };
var source = { 'greeting': 'hi' };
 
_.isMatchWith(object, source, customizer);
// => true
```

## 判断 大小

### lt（判断是否小）

```javascript
_.lt(value, other);
```
```javascript
_.lt(1, 3);
// => true
 
_.lt(3, 3);
// => false
 
_.lt(3, 1);
// => false
```

### lte（判断是否小于等于）

```javascript
_.lte(value, other)
```
```javascript
_.lte(1, 3);
// => true
 
_.lte(3, 3);
// => true
 
_.lte(3, 1);
// => false
```

### gt（判断是否大）

```javascript
_.gt(value, other)
```
```javascript
_.gt(3, 1);
// => true
 
_.gt(3, 3);
// => false
 
_.gt(1, 3);
// => false
```

### gte（判断是否大于等于）

```javascript
_.gte(value, other);
```
```javascript
_.gte(3, 1);
// => true
 
_.gte(3, 3);
// => true
 
_.gte(1, 3);
// => false
```

## 是否是 arguments

### isArguments

```javascript
_.isArguments(value);
```
```javascript
_.isArguments(function() { return arguments; }());
// => true
 
_.isArguments([1, 2, 3]);
// => false
```

## 是否是 数组

### isArray

```javascript
_.isArray(value);
```
```javascript
_.isArray([1, 2, 3]);
// => true
 
_.isArray(document.body.children);
// => false
 
_.isArray('abc');
// => false
 
_.isArray(_.noop);
// => false
```

## 是否是 类数组

### isArrayLike

```javascript
_.isArrayLike(value);
```
```javascript
_.isArrayLike([1, 2, 3]);
// => true
 
_.isArrayLike(document.body.children);
// => true
 
_.isArrayLike('abc');
// => true
 
_.isArrayLike(_.noop);
// => false
```

### isArrayLikeObject
> 类似 isArrayLike，若值为对象也为 true

```javascript
_.isArrayLikeObject(value);
```
```javascript
_.isArrayLikeObject([1, 2, 3]);
// => true
 
_.isArrayLikeObject(document.body.children);
// => true
 
_.isArrayLikeObject('abc');
// => false
 
_.isArrayLikeObject(_.noop);
// => false
```

## 是否是 ArrayBuffer

### ArrayBuffer

```javascript
_.isArrayBuffer(value);
```
```javascript
_.isArrayBuffer(new ArrayBuffer(2));
// => true
 
_.isArrayBuffer(new Array(2));
// => false
```

## 是否是 Boolean 类型

### isBoolean

```javascript
_.isBoolean(value);
```
```javascript
_.isBoolean(false);
// => true
 
_.isBoolean(null);
// => false
```

## 是否是 Buffer 类型

### isBuffer

```javascript
_.isBuffer(value);
```
```javascript
_.isBuffer(new Buffer(2));
// => true
 
_.isBuffer(new Uint8Array(2));
// => false
```

## 是否是 Date 类型

### isDate

```javascript
_.isDate(value);
```
```javascript
_.isDate(new Date); 
// => true
 
_.isDate('Mon April 23 2012');
// => false
```

## 是否是 Dom 元素

### isElement

```javascript
_.isElement(value);
```
```javascript
_.isElement(document.body);
// => true
 
_.isElement('<body>');
// => false
```

## 是否是 Error 类型

### isError

```javascript
_.isError(value);
```
```javascript
_.isError(new Error);
// => true
 
_.isError(Error);
// => false
```

## 是否是 有限数值

### isFinite

```javascript
_.isFinite(value);
```
```javascript
_.isFinite(3);
// => true
 
_.isFinite(Number.MIN_VALUE);
// => true
 
_.isFinite(Infinity);
// => false
 
_.isFinite('3');
// => false
```

## 是否是 有效长度

### isLength

```javascript
_.isLength(value)
```
```javascript
_.isLength(3);
// => true
 
_.isLength(Number.MIN_VALUE);
// => false
 
_.isLength(Infinity);
// => false
 
_.isLength('3');
// => false
```

## 是否是 Function 类型

### isFunction

```javascript
_.isFunction(value)
```
```javascript
_.isFunction(_);
// => true
 
_.isFunction(/abc/);
// => false
```

## 是否是 Map 类型

### isMap

```javascript
_.isMap(value)
```
```javascript
_.isMap(new Map);
// => true
 
_.isMap(new WeakMap);
// => false
```

## 是否是 整数

### isInteger

```javascript
_.isInteger(value);
```
```javascript
_.isInteger(3);
// => true
 
_.isInteger(Number.MIN_VALUE);
// => false
 
_.isInteger(Infinity);
// => false
 
_.isInteger('3');
// => false
```

## 是否是 空对象、空集合

### isEmpty
> 传入其他类型的值，结果为 true

```javascript
_.isEmpty(value);
```
```javascript
_.isEmpty(null);
// => true
 
_.isEmpty(true);
// => true
 
_.isEmpty(1);
// => true
 
_.isEmpty([1, 2, 3]);
// => false
 
_.isEmpty({ 'a': 1 });
// => false
```

## 是否是 NaN

### isNaN

```javascript
_.isNaN(value);
```
```javascript
_.isNaN(NaN);
// => true
 
_.isNaN(new Number(NaN));
// => true
 
isNaN(undefined);
// => true
 
_.isNaN(undefined);
// => false
```

## 是否是 原生函数

### isNative

```javascript
_.isNative(value)
```
```javascript
_.isNative(Array.prototype.push);
// => true
 
_.isNative(_);
// => false
```

## 是否是 undefined 或 null

### isNil

```javascript
_.isNil(value)
```
```javascript
_.isNil(null);
// => true
 
_.isNil(void 0);
// => true
 
_.isNil(NaN);
// => false
```

## 是否是 Number 类型

### isNumber

```javascript
_.isNumber(value)
```
```javascript
_.isNumber(3);
// => true
 
_.isNumber(Number.MIN_VALUE);
// => true
 
_.isNumber(Infinity);
// => true
 
_.isNumber('3');
// => false
```

## 是否是 Object

### isObject

```javascript
_.isObject(value);
```
```javascript
_.isObject({});
// => true
 
_.isObject([1, 2, 3]);
// => true
 
_.isObject(_.noop);
// => true
 
_.isObject(null);
// => false
```

## 是否是 类对象

### isObjectLike

```javascript
_.isObjectLike(value)
```
```javascript
_.isObjectLike({});
// => true
 
_.isObjectLike([1, 2, 3]);
// => true
 
_.isObjectLike(_.noop);
// => false
 
_.isObjectLike(null);
// => false
```

## 是否是 普通对象

### isPlainObject

```javascript
_.isPlainObject(value)
```
```javascript
function Foo() {
  this.a = 1;
}
 
_.isPlainObject(new Foo);
// => false
 
_.isPlainObject([1, 2, 3]);
// => false
 
_.isPlainObject({ 'x': 0, 'y': 0 });
// => true
 
_.isPlainObject(Object.create(null));
// => true
```

## 是否是 RegExp 类型

### isRegExp

```javascript
_.isRegExp(value)
```
```javascript
_.isRegExp(/abc/);
// => true
 
_.isRegExp('/abc/');
// => false
```

## 是否是 安全整数

### isSafeInteger

```javascript
_.isSafeInteger(value);
```
```javascript
_.isSafeInteger(3);
// => true
 
_.isSafeInteger(Number.MIN_VALUE);
// => false
 
_.isSafeInteger(Infinity);
// => false
 
_.isSafeInteger('3');
// => false
```

## 是否是 Set 类型

### isSet

```javascript
_.isSet(value)
```
```javascript
_.isSet(new Set);
// => true
 
_.isSet(new WeakSet);
// => false
```

## 是否是 String 类型

### isString

```javascript
_.isString(value);
```
```javascript
_.isString('abc');
// => true
 
_.isString(1);
// => false
```

## 是否是 Symbol 类型

### isSymbol

```javascript
_.isSymbol(value);
```
```javascript
_.isSymbol(Symbol.iterator);
// => true
 
_.isSymbol('abc');
// => false
```

## 是否是 TypedArray 类型

### isTypedArray

```javascript
_.isTypedArray(value);
```
```javascript
_.isTypedArray(new Uint8Array);
// => true
 
_.isTypedArray([]);
// => false
```

## 是否是 Undefined

### isUndefined

```javascript
_.isUndefined(value);
```
```javascript
_.isUndefined(void 0);
// => true
 
_.isUndefined(null);
// => false
```

## 是否是 WeakMap 类型

### isWeakMap

```javascript
_.isWeakMap(value);
```
```javascript
_.isWeakMap(new WeakMap);
// => true
 
_.isWeakMap(new Map);
// => false
```

## 是否是 WeakSet 类型

### isWeakSet

```javascript
_.isWeakSet(value)
```
```javascript
_.isWeakSet(new WeakSet);
// => true
 
_.isWeakSet(new Set);
// => false
```