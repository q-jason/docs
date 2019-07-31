## 列表页标签
> 注意 orderby = 'weight'，默认好像无效（未测试），需要自己写 php 代码（百度即可找到）

```
{dede:list titlelen='1000' infolen='1000' orderby='' pagesize=''}
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
  
{/dede:list}
```

 参数名     | 介绍
 -----     | ---------------------------------------
 col       | 用于实现多列显示，值为当前列数（默认为1，表示单列）
 titlelen  | 标题长度
 infolen   | 内容摘要长度
 imgwidth  | 缩略图宽度
 imgheight | 缩略图高度
 orderby   | 排序方式
 pagesize  | 分页大小，调用文章条数
 orderway  | 值为 desc 或 asc ，指定排序方式是降序还是顺向排序，默认为降序
 noflag    | 不匹配的标签
 
 
 
## 分页标签
> 大部分情况需要定制，下面是定制过程

```
{dede:pagelist/}
{dede:pagelist istitem="index,pre,next,end,info," listsize="5"/}
```

#### 普通列表页面
1. 找到 /include/arc.listview.class.php
2. 找到 GetPageListST（静态） 和 GetPageListDM（动态） 函数
> 需要同时修改，否则只会动态或静态预览有效
3. 按照需要更改结构即可
> 注意，最好按需修改，不要直接赋值动态到静态，否则链接会错误（未知原因，暂未深究）

#### 搜索结果页面
1. 找到 /include/arc.searchview.class.php
2. 找到 GetPageListDM 函数

```php
  function GetPageListST($list_len, $listitem = "index,end,pre,next,pageno") {
    //.. 同下 ..
  }
  function GetPageListDM($list_len, $listitem = "index,end,pre,next,pageno") {
    ...
    
    // 这里改变上一页下一页的结构
    if ($this->PageNo != 1) {
      $prepage .= "<a href='" . $purl . "PageNo=$prepagenum'>&lt;</a>\r\n";
      $indexpage = "<a class='cpagination-item' href='" . $purl . "PageNo=1'>&lt;&lt;</a>\r\n";
    } else {
      $indexpage = "<a class='cpagination-item'>&lt;&lt;</a>\r\n";
    }
    if ($this->PageNo != $totalpage && $totalpage > 1) {
      $nextpage .= "<a href='" . $purl . "PageNo=$nextpagenum'>下一页</a>\r\n";
    } else {
      $endpage = "";
    }
    
    ...
    
    // 这里更改索引的结构
    for ($j; $j <= $total_list; $j++) {
      if ($j == $this->PageNo) {
        $listdd .= "<a class='cpagination-nav-item active'>$j</a>\r\n";
      } else {
        $listdd .= "<a class='cpagination-nav-item' href='" . str_replace("{page}", $j, $tnamerule) . "'>" . $j . "</a>\r\n";
      }
    }
    
    // 手动拼接结构
    $plist = "
          <section class='cpagination'>
            <div class='cpagination-wrapper'>
              <div class='cpagination-nav'>
                " . $listdd . "
              </div>
                " . $nextpage . "
                " . $endpage . "
            </div>
          </section>
        ";
     
    // 弃用原始拼接
    // if (preg_match('/index/i', $listitem)) $plist .= $indexpage;
    // if (preg_match('/pre/i', $listitem)) $plist .= $prepage;
    // if (preg_match('/pageno/i', $listitem)) $plist .= $listdd;
    // if (preg_match('/next/i', $listitem)) $plist .= $nextpage;
    // if (preg_match('/end/i', $listitem)) $plist .= $endpage;
    // if (preg_match('/option/i', $listitem)) $plist .= $optionlist;
    // if (preg_match('/info/i', $listitem)) $plist .= $maininfo;
    
    return $plist;
  }
```

------------------------------------------------------------