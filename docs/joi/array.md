## 检查数组项中的值
> https://joi.dev/api/?v=17.4.0#arrayitemstypes
```javascript
items(/* 看官方文档吧 */);
```

## 检查是否是唯一值数组
> https://joi.dev/api/?v=17.4.0#arrayuniquecomparator-options
```javascript
unique((a, b) => a === b);
// => array.unique
```

## 检查长度
```javascript
min(2)
// => array.min
max(10)
// => array.max
length(5)
// => array.length
```