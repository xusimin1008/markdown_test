### 数据积累
> 股票

> 豆瓣电影top 250

### 查看谷歌扩展的代码
```
cd Library/Application\ Support/Google/Chrome/Default/Extensions
在谷歌扩展程序中 开启 开发者模式 得到扩展id
到上面的目录找到id对应的目录，里面即为源码
```
### amazon爬虫
```
存储路径（对象存储）：Amz{region(Us, Cn, Uk)}/{year}/{month}/{date}/{asin}.{format(html, xml)}.gz

抓取来源：按各品类去抓取和用户自定义添加
-- 用户添加的商品等到下一次抓取周期才进行

抓取时间间隔：固定（假设每3，5或者7天抓取一次商品排行榜和商品快照）
-- 现在的抓取时间间隔只能保证是我们想要的间隔，但并不能保证在我们想要的时间内，即如果出现这样的异常作何处理？

面对不同结构的页面，应该把所有情况都尝试一遍，比如，detail = ''
if (!detail) { ... }
if (!detail) { ... }
...

```

### amazon category 研究
```
Clothing下的Women的Shorts的node_id为：1048186, 在Men下的node_id 为：1045560
说明 -- 具有相同名称的子品类在不同较大品类下中的node_id也是不同的。
---
在四个排行榜下的品类展示都是一样的，除了movers and shakers只展示最高品类，
所以要想抓取所有的品类，只需抓取某一个，如best sellers下的品类。
```
存储结构
```
id, dept_code, parent_id, node_id, name,
best_sellers_url, crawled_best_sellers_at,
hot_new_releases_url, crawled_hot_new_releases_at
movers_and_shakers_url, crawled_movers_and_shakers_at
most_wished_for_url, crawled_most_wished_for_at
most_gifted_url, crawled_most_gifted_at
```

### vue相关
```
v-cloak 不显示元素知道编译完成
v-text 显示元素内容 <span v-text="msg"></span> == <span>{{msg}}</span> （不过后者在元素未编译完成时会显示{{msg}}，建议使用前者）

```
### pg数据库语句
```
update products set review_url = replace(review_url, 'helpful', 'recent&pageNumber=1'); (替换字符串)
```

###laravel学习
```
php composer.phar dumpautoload  (数据库重建时，某些表出现错误)
```

### tornado学习
> 想了解框架和学习一下消息推送

***

### Cron正则表达式检查
```
<?php
$cron = "*/5 * * * *";
$result = preg_match(
	"/(\*|[0-5]?[0-9]|\*\/[0-9]+)\s+"
	."(\*|1?[0-9]|2[0-3]|\*\/[0-9]+)\s+"
	."(\*|[1-2]?[0-9]|3[0-1]|\*\/[0-9]+)\s+"
	."(\*|[0-9]|1[0-2]|\*\/[0-9]+|jan|feb|mar|apr|may|jun|jul|aug|sep|oct|nov|dec)\s+"
	."(\*\/[0-9]+|\*|[0-7]|sun|mon|tue|wed|thu|fri|sat)\s*/i", $cron, $matches); （不支持逗号）
	
$pattern = '^((?:[1-9]?\d|\*)\s*(?:(?:[\/-][1-9]?\d)|(?:,[1-9]?\d)+)?\s*){5}$'; (完整可用的)
```
***

### 清空redis的某个数据库
```
  $ redis-cli 
  > select [db_num]
  > flushdb
```
