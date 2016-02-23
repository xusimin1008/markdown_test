### 数据积累
> 股票

> 豆瓣电影top 250

### amazon category 研究
```
Clothing下的Women的Shorts的node_id为：1048186, 在Men下的node_id 为：1045560
说明 -- 具有相同名称的子品类在不同较大品类下中的node_id也是不同的。
```

### vue相关
```
v-cloak 不显示元素知道编译完成
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
