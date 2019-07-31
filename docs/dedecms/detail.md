## 详情页标签

```
// 文章链接
{dede:field name='arcurl'/}

// 文章标题
{dede:field.title/}

// 简短描述
{dede:field.description}

// 发布时间
{dede:field.pubdate function="MyDate('Y-m-d H:i',@me)"/}
{dede:field.pubdate function="MyDate('Y-m-d',@me)"/}

// 文章正文内容
{dede:field.body/}

// 上一篇
{dede:prenext get='pre'/}

// 下一篇
{dede:prenext get='next'/}
```