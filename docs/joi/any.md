## 只允许某些值
```javascript
valid(...params)
equal(...params)
// => any.only
```

## 不允许某些值
```javascript
invalid(...values)
disallow(...values)
not(...values)
```

### 必须定义值，并且值不能为空
> 有可能报错的状态码为 string.empty（定义了，但是为空值）
```javascript
required()
// any.required
// string.empty
```