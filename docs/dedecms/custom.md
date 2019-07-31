## newchannel（韩哥）
> channel 升级版，支持子级调用，并且 active 或 hover 样式 <br/>
> 目前会出现 \[field:active] \[field:hover] 同时多个的问题，需要修改数据库中的一个 id 字段

```
{dede:newchannel type='top' typeid='1,2,3'}
  <a href="[field:typeurl/] " class="[field:current/] [field:hover/] [field:active/]">
    [field:typename/]
  </a>
  
  [field:sonchannel0]
  <li>
    <a href="[field:typeurl/]">[field:typename/]</a>
    <ul>
      [field:sonchannel1]
      <li><a href="[field:typeurl/]">[field:typename/]</a></li>
      [/field:sonchannel1]
    </ul>
  </li>
  [/field:sonchannel0]

{/dede:newchannel} 
```