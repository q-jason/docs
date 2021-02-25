## 引言
本文档只记录常用的方法以及心得

## 链接
- [Document](https://joi.dev/api/)
- [Github](https://github.com/sideway/joi#readme)

## 使用经验
### validate 方法常用参数
```javascript
let { error, value } = schema.validate(data, {
  // 允许检查的对象包含未定义规则的字段
  allowUnknown: false,

  // 在检查到第一个错误后，就会停止检查，只返回第一个的错误信息
  abortEarly: true,

  // 检查前，会先将值尝试转换
  // 建议开启，内部的很多方法（如 trim），都基于这个参数进行转换
  convert: true,

  // 返回的 value 是通过检测对象浅克隆出来的
  nonEnumerables: false
})
```

### 自定义校验规则
```javascript
// 自定义校验规则
// https://joi.dev/api/?v=17.4.0#anycustommethod-description
custom((value, helper) => {
  // 验证值...
  // 若出错，通过 helper 生成错误并返回，参数为错误码（必须要传递的）
  return helpers.error('phone.invalid')
  // 若正确，返回值
  return value
})
```

### 替换默认报错消息
> 这里不能使用 message <br/>
> 因为 message 方法很多的 "前缀方法" 都不支持，比如说 required 和 empty。
```
来自官方文档的话：
https://joi.dev/api/?v=17.4.0#anyruleoptions

Rule modifications can only be applied to supported rules. 
Most of the any methods do not support rule modifications because they are implemented 
using schema flags (e.g. required()) or special internal implementation (e.g. valid()). 
In those cases, use the any.messages() method to override 
the error codes for the errors you want to customize.
```
```javascript
// messages 参数可以通过全局的方式统一定义复用
// 因为他是通过模板字符串去渲染的，只要定义好 label 即可

const defaultMessage = { 
  'any.required': '{{ #label }} 不能为空',
  'string.empty': '{{ #label }} 不能为空',
  'string.min': '{{ #label }} 长度最小为 {{ #limit }} 位',
  'string.max': '{{ #label }} 长度最大为 {{ #limit }} 位 '
}

Joi.string()
  .label('用户名')
  .required()
  .empty()
  .min(4)
  .max(10)
  .messages(defaultMessage)
```

### 对象风格检验

#### 同步
```javascript
let schema = Joi.object({
  // username 可参考 "替换默认报错消息" 中的定义
  username
})
let { error, value } = schema.validate({ username: 'jason' });

if (error) console.log(error.message)
```

#### 异步
```javascript
let schema = Joi.object({
  // username 可参考 "替换默认报错消息" 中的定义
  username
})
try {
  let value = schema.validateAsync({ username: 'jason' });
}
catch (err) {
  console.log(err.message)
}
```

### 单一值检验

#### 同步
```javascript
// username 可参考 "替换默认报错消息" 中的定义
let { error, value } = username.validate('jason');

if (error) console.log(error.message)
```

#### 异步
```javascript
try {
  // username 可参考 "替换默认报错消息" 中的定义
  let value = username.validateAsync('jason');
}
catch (err) {
  console.log(err.message)
}
```