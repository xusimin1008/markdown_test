### 数据积累
> 股票


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
