## 必须并且只能同时存在一个 key
```javascript
xor('k1', 'k2', 'k3')
// => object.xor
````

## 至少出现一个指定的字段
```javascript
or('k1', 'k2', 'k3')
// => object.missing
```

## key 存在时，附属的 key 也必须存在
```javascript
with(key, 'k1');
// => object.with
```

## 当 key 存在时，不允许出现其他的指定 key
```javascript
without(key, [ 'k1', 'k2' ])
// => object.without
```

## 若其中一个存在，则全部都要存在
> 允许都不存在的情况
```javascript
and('k1', 'k2', 'k3')
// => object.and
```

## 不能同时存在
> 允许都不存在的情况
```javascript
nand('k1', 'k2', 'k3')
// => object.nand
````

## 要求对象必须是某类的实例
```javascript
instance(RegExp)
// => object.instance
```

## 验证对象中 key 的个数
```javascript
min(5)
// => object.min
max(10)
// => object.max
length(7)
// => object.length
```