## 网站根目录
```
{dede:global.cfg_cmsurl/}
```

## 调用指定模板
```
{dede:include filename="xxx.htm"/}
```

## 调用单个栏目
```
{dede:type typeid='0'}[field:typename/]{/dede:type}
{dede:type typeid='0'}[field:typelink/]{/dede:type}
{dede:type typeid='0'}[field:seotitle/]{/dede:type}
```

## 调用多个栏目
```
{dede:channel type="son" typeif="10" currentstyle="
  <li class='hover'>
    <a href='~typelink~' ~rel~>
      <span>~typename~</span>
    </a>
  </li>
"}
  <li>
    <a href='[field:typeurl/]' [field:rel/]>
      <span>[field:typename/]</span>
    </a>
  </li>
{/dede:channel}
```

 参数名       | 描述
 ------------ | --------------------------------------------
 type         | top（顶级栏目），son（下级）
 col          | 实现多列
 row          | 显示多少个
 type         | 指定 id
 currentstyle | 激活样式
 
 
 
 
 
 
## 循环调用
```
调用所有一级栏目和二级栏目
{dede:channelartlist type="top" typeid='top'}
  {dede:field name='typeurl'/}
  {dede:field name='typename'/}
  {dede:channel}
  <ul>
    <li>
      <a href="[field:typeurl/]">
        [field:typename/]
      </a>
    </li>
  </ul>
  {/dede:channel}
{/dede:channelartlist}

调用指定栏目的子级栏目，并调用子级栏目的内容
若 typeid 为 0 标识当前栏目
{dede:channelartlist type="son" typeid='1, 2, 3'}
  {dede:field name='typeurl'/}
  {dede:field name='typename'/}
  <ul>
    {dede:arclist}
      <li>
        <a href="[field:typeurl/]">
          [field:typename/]
        </a>
      </li>
    {/dede:arclist}
  </ul>
{/dede:channelartlist}
```

## 调用当前位置
> 定制待写

```
{dede:field name='position'/}
```

## 获取指定栏目的文章列表
> 注意：arclist 标签 不分页 <br/>
> 注意 orderby = 'weight'，默认好像无效（未测试），需要自己写 php 代码（百度即可找到） <br/>

```
{dede:arclist flag='h' typeid='' row='' col='' titlelen='' infolen='' imgwidth='' imgheight='' listtype='' orderby='' keyword='' limit='0,1'}
  // 所属栏目名
  [field:typename/]
  
  // 所属栏目链接
  [field:typelink/]
  
  // 文章链接
  [field:arcurl/]
  
  // 文章标题
  [field:title/]
  // 文章标题 限制字数溢出 ... 显示
  [field:title function='( strlen("@me")>115 ? cn_substr("@me",110)."..." : "@me" )'/]
  
  // 文章描述
  [field:description/]
  // 限制字数溢出 ... 显示
  [field:description function='( strlen("@me")>115 ? cn_substr("@me",110)."..." : "@me" )'/]
  
  // 文章缩略图
  [field:picname/]
  
  // 文章发布日期
  // 2012-12-27 18:30:02
  [field:pubdate function="GetDateTimeMK(@me)" /]
  // 2009-12-27
  [field:pubdate function="GetDateMK(@me)"/] 
  // 定制格式
  [field:pubdate function='strftime("%y-%m-%d",@me)'/]
{/dede:arclist}
```

 参数名     | 介绍
 -----     | ---------------------------------------
 col       | 用于实现多列显示，值为当前列数（默认为1，表示单列）
 row       | 返回文档列表总数
 typeid    | 栏目ID,在列表模板和档案模板中一般不需要指定，在首页模板中允许用 ”,” 分开表示多个栏目
 getall    | 在没有指定这属性的情况下,在栏目页、文章页模板,不会获取以”,”分开的多个栏目的下级子类
 titlelen  | 标题长度
 infolen   | 内容摘要长度
 imgwidth  | 缩略图宽度
 imgheight | 缩略图高度
 orderby   | 排序方式
 keyword   | 含有指定关键字的文档列表，多个关键字用 ',' 分
 limit     | 起始ID,记录数 （如：limit=’1,2′  表示从ID为1的记录开始，取2条记录）
 flag      | 自定义属性值：头条[h] 推荐[c] 图片[p] 幻灯[f] 滚动[s] 跳转[j] 图文[a] 加粗[b]
 noflag    | 同flag，但这里是表示不包含这些属性
 orderway  | 值为 desc 或 asc ，指定排序方式是降序还是顺向排序，默认为降序
 subday    | 表示在多少天以内的文档
 aid       | 没理解啥意思。。指定文档ID
 idlist    | 没理解啥意思。。提取特定文档（文档ID）
 channelid | 没理解啥意思。。频道ID

----------------------------------------------------

## 搜索功能
> 实现步骤如下

1. 新建 search.htm 放到 /templets/default/ 目录中
> search.htm 就按照列表页面写标签即可

```
// 调用搜索关键词
{dede:global name='keyword'/}

// 搜索结果
{dede:list titlelen='1000' infolen='1000' orderby='weight' pagesize='10'}
...
{/dede:list}

// 分页
{dede:pagelist/}
```
2. 在网页中需要搜索的位置加入 html 代码，如下

```html
<!-- 地址为 /plus/search.php -->
<form method="get" action="{dede:global.cfg_cmsurl/}/plus/search.php">
  <!-- 关键词输入框，注意 name 为 q -->
  <input name="q" type="text">
  <input type="submit">
</form>
```

## 自增（索引判断）

```
[field:global name=autoindex runphp="yes"](@me%2==0)? @me="|":@me="";[/field:global]
```