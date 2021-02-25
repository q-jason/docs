## 邮箱判断
> https://joi.dev/api/?v=17.4.0#stringemailoptions
```javascript
email(/* ..一堆参数.. */);
// => string.email
````

## 开头和结尾不能包含空格
> 若 validate 时 convert 为 true，则会尝试转换
```javascript
trim()
// => string.trim
```

## 只能小写或大写
> 若 validate 时 convert 为 true，则会尝试转换
```javascript
lowercase();
// string.lowercase
uppercase();
// string.uppercase
```

## 指允许 a-z A-Z 0-9
```javascript
alphanum()
// => string.alphanum
```

## 只允许 a-z A-Z 0-9 _
```javascript
token()
// => string.token
```

## length 限制
```javascript
min(5)
// => string.min

max(10)
// => string.max

length(7)
// => string.length
```