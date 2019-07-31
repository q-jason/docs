## 检查

### startsWith（开头检查，指定字符串）

```javascript
_.startsWith([string=''], [target], [position=0]);
```
```javascript
_.startsWith('abc', 'a');
// => true
 
_.startsWith('abc', 'b');
// => false
 
_.startsWith('abc', 'b', 1);
// => true
```

### endsWith（结尾检查，指定字符串）

```javascript
_.endsWith([string=''], [target], [position=string.length]);
```
```javascript
_.endsWith('abc', 'c');
// => true
 
_.endsWith('abc', 'b');
// => false
 
_.endsWith('abc', 'b', 2);
// => true
```

## 长度限制

### truncate（溢出后，显示指定字符串）

```javascript
// [string=''] (string): 要截断的字符串。
// [options={}] (Object): 选项对象。
// [options.length=30] (number): 允许的最大长度。
// [options.omission='...'] (string): 超出后的代替字符。
// [options.separator] (RegExp|string): 截断点。
_.truncate([string=''], [options={}]);
```
```javascript
_.truncate('hi-diddly-ho there, neighborino');
// => 'hi-diddly-ho there, neighbo...'
 
_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': ' '
});
// => 'hi-diddly-ho there,...'
 
_.truncate('hi-diddly-ho there, neighborino', {
  'length': 24,
  'separator': /,? +/
});
// => 'hi-diddly-ho there...'
 
_.truncate('hi-diddly-ho there, neighborino', {
  'omission': ' [...]'
});
// => 'hi-diddly-ho there, neig [...]'
```

## 基于原生的

### replace（同 String.prototype.replace）

```javascript
_.replace([string=''], pattern, replacement)
```
```javascript
_.replace('Hi Fred', 'Fred', 'Barney');
// => 'Hi Barney'
```

### split（按照指定字符拆分为数组）

```javascript
_.split([string=''], separator, [limit]);
```
```javascript
_.split('a-b-c', '-', 2);
// => ['a', 'b']
```

### toLower（转为小写）

```javascript
_.toLower([string=''])
```
```javascript
_.toLower('--Foo-Bar--');
// => '--foo-bar--'
 
_.toLower('fooBar');
// => 'foobar'
 
_.toLower('__FOO_BAR__');
// => '__foo_bar__'
```

### toUpper（转为大写）

```javascript
_.toUpper([string=''])
```
```javascript
_.toUpper('--foo-bar--');
// => '--FOO-BAR--'
 
_.toUpper('fooBar');
// => 'FOOBAR'
 
_.toUpper('__foo_bar__');
// => '__FOO_BAR__'
```

## 命名规则转换

### camelCase（驼峰命名）

```javascript
_.camelCase([string='']);
```
```javascript
_.camelCase('Foo Bar');
// => 'fooBar'
 
_.camelCase('--foo-bar--');
// => 'fooBar'
 
_.camelCase('__FOO_BAR__');
// => 'fooBar'
```

### kebabCase（短横线命名）

```javascript
_.kebabCase([string='']);
```
```javascript
_.kebabCase('Foo Bar');
// => 'foo-bar'
 
_.kebabCase('fooBar');
// => 'foo-bar'
 
_.kebabCase('__FOO_BAR__');
// => 'foo-bar'
```

### snakeCase（下划线命名）

```javascript
_.snakeCase([string='']);
```
```javascript
_.snakeCase('Foo Bar');
// => 'foo_bar'
 
_.snakeCase('fooBar');
// => 'foo_bar'
 
_.snakeCase('--FOO-BAR--');
// => 'foo_bar'
```

### lowerCase（小写命名）

```javascript
_.lowerCase([string='']);
```
```javascript
_.lowerCase('--Foo-Bar--');
// => 'foo bar'
 
_.lowerCase('fooBar');
// => 'foo bar'
 
_.lowerCase('__FOO_BAR__');
// => 'foo bar'
````

### startCase（单词开头大写，空格分割单词）

```javascript
_.startCase([string='']);
```
```javascript
_.startCase('--foo-bar--');
// => 'Foo Bar'
 
_.startCase('fooBar');
// => 'Foo Bar'
 
_.startCase('__FOO_BAR__');
// => 'FOO BAR'
```

### upperCase（全单词大写，空格分割单词）

```javascript
_.upperCase([string='']);
```
```javascript
_.upperCase('--foo-bar');
// => 'FOO BAR'
 
_.upperCase('fooBar');
// => 'FOO BAR'
 
_.upperCase('__foo_bar__');
// => 'FOO BAR'
```

### capitalize（首字母大写，其余小写）

```javascript
_.capitalize([string=''])
```
```javascript
_.capitalize('FRED');
// => 'Fred'
```

### lowerFirst（首字母小写，其余不变）

```javascript
_.lowerFirst([string='']);
```
```javascript
_.lowerFirst('Fred');
// => 'fred'
 
_.lowerFirst('FRED');
// => 'fRED'
```

### upperFirst（首字母大写，其余不变）

```javascript
_.upperFirst([string='']);
```
```javascript
_.upperFirst('fred');
// => 'Fred'
 
_.upperFirst('FRED');
// => 'FRED'
````

## 转义

### escape（转义特殊字符为 html 实体字符）

```javascript
_.escape([string='']);
```
```javascript
_.escape('fred, barney, & pebbles');
// => 'fred, barney, &amp; pebbles'
```

### unescape（转义 html 实体字符为特殊字符）

```javascript
_.unescape([string='']);
```
```javascript
_.unescape('fred, barney, &amp; pebbles');
// => 'fred, barney, & pebbles'
```

### escapeRegExp（转义 RegExp 字符串中的特殊字符）

```javascript
_.escapeRegExp([string='']);
```
```javascript
_.escapeRegExp('[lodash](https://lodash.com/)');
// => '\[lodash\]\(https://lodash\.com/\)'
```

### deburr（拉丁语）

```javascript
_.deburr([string='']);
```
```javascript
_.deburr('déjà vu');
// => 'deja vu'
```

## 移除和填充

### trim（左右两侧移除空格，或指定字符）

```javascript
_.trim([string=''], [chars=whitespace]);
```
```javascript
_.trim('  abc  ');
// => 'abc'
 
_.trim('-_-abc-_-', '_-');
// => 'abc'
 
_.map(['  foo  ', '  bar  '], _.trim);
// => ['foo', 'bar']
```

### trimStart（左侧移除空格，或指定字符）

```javascript
_.trimStart([string=''], [chars=whitespace]);
```
```javascript
_.trimStart('  abc  ');
// => 'abc  '
 
_.trimStart('-_-abc-_-', '_-');
// => 'abc-_-'
```

### trimEnd（右侧移除空格，或指定字符）

```javascript
_.trimEnd([string=''], [chars=whitespace]);
```
```javascript
_.trimEnd('  abc  ');
// => '  abc'
 
_.trimEnd('-_-abc-_-', '_-');
// => '-_-abc'
```

### pad（左右两侧填充指定字符）

```javascript
_.pad([string=''], [length=0], [chars=' ']);
```
```javascript
_.pad('abc', 8);
// => '  abc   '
 
_.pad('abc', 8, '_-');
// => '_-abc_-_'
 
_.pad('abc', 3);
// => 'abc'
```

### padStart（左侧填充指定字符）

```javascript
_.padStart([string=''], [length=0], [chars=' ']);
```
```javascript
_.padStart('abc', 6);
// => '   abc'
 
_.padStart('abc', 6, '_-');
// => '_-_abc'
 
_.padStart('abc', 3);
// => 'abc'
```

### padEnd（右侧填充指定字符）

```javascript
_.padEnd([string=''], [length=0], [chars=' ']);
```
```javascript
_.padEnd('abc', 6);
// => 'abc   '
 
_.padEnd('abc', 6, '_-');
// => 'abc_-_'
 
_.padEnd('abc', 3);
// => 'abc'
```

## 重复拼接

### repeat（重复 n 次给定的字符串）

```javascript
_.repeat([string=''], [n=1]);
```
```javascript
_.repeat('*', 3);
// => '***'
 
_.repeat('abc', 2);
// => 'abcabc'
 
_.repeat('abc', 0);
// => ''
```

## 拆分字符串中的单词为数组

### words

```javascript
_.words([string=''], [pattern]);
```
```javascript
_.words('fred, barney, & pebbles');
// => ['fred', 'barney', 'pebbles']
 
_.words('fred, barney, & pebbles', /[^, ]+/g);
// => ['fred', 'barney', '&', 'pebbles']
```

## 模板

### template（强大的模板语言...）

```javascript
_.template([string=''], [options={}]);
```
```javascript
// 使用 "interpolate" 分隔符创建编译模板
var compiled = _.template('hello <%= user %>!');
compiled({ 'user': 'fred' });
// => 'hello fred!'
 
// 使用 HTML "escape" 转义数据的值
var compiled = _.template('<b><%- value %></b>');
compiled({ 'value': '<script>' });
// => '<b>&lt;script&gt;</b>'
 
// 使用 "evaluate" 分隔符执行 JavaScript 和 生成HTML代码
var compiled = _.template('<% _.forEach(users, function(user) { %><li><%- user %></li><% }); %>');
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
 
// 在 "evaluate" 分隔符中使用内部的 `print` 函数
var compiled = _.template('<% print("hello " + user); %>!');
compiled({ 'user': 'barney' });
// => 'hello barney!'
 
// 使用 ES 分隔符代替默认的 "interpolate" 分隔符
var compiled = _.template('hello ${ user }!');
compiled({ 'user': 'pebbles' });
// => 'hello pebbles!'
 
// 使用自定义的模板分隔符
_.templateSettings.interpolate = /{{([\s\S]+?)}}/g;
var compiled = _.template('hello {{ user }}!');
compiled({ 'user': 'mustache' });
// => 'hello mustache!'
 
// 使用反斜杠符号作为纯文本处理
var compiled = _.template('<%= "\\<%- value %\\>" %>');
compiled({ 'value': 'ignored' });
// => '<%- value %>'
 
// 使用 `imports` 选项导入 `jq` 作为 `jQuery` 的别名
var text = '<% jq.each(users, function(user) { %><li><%- user %></li><% }); %>';
var compiled = _.template(text, { 'imports': { 'jq': jQuery } });
compiled({ 'users': ['fred', 'barney'] });
// => '<li>fred</li><li>barney</li>'
 
// 使用 `sourceURL` 选项指定模板的来源URL
var compiled = _.template('hello <%= user %>!', { 'sourceURL': '/basic/greeting.jst' });
compiled(data);
// => 在开发工具的 Sources 选项卡 或 Resources 面板中找到 "greeting.jst"
 
// 使用 `variable` 选项确保在编译模板中不声明变量
var compiled = _.template('hi <%= data.user %>!', { 'variable': 'data' });
compiled.source;
// => function(data) {
//   var __t, __p = '';
//   __p += 'hi ' + ((__t = ( data.user )) == null ? '' : __t) + '!';
//   return __p;
// }
 
// 使用 `source` 特性内联编译模板
// 便以查看行号、错误信息、堆栈
fs.writeFileSync(path.join(cwd, 'jst.js'), '\
  var JST = {\
    "main": ' + _.template(mainText).source + '\
  };\
');
```