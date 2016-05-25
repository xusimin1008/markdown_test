邮箱：
```
night10081503@163.com
night_and_leslie@163.com
```

```
scrapy:
Extensions里面的spider_error只会记录spider的错误，并不会记录pipeline内的错误
DownloaderMiddleware中如果请求为重定向时，重定向后的request会把meta都丢失
```

```
按enter不触发表单提交
<form onsubmit="return false;">

<script>
var submitHandler = function() {
  // do stuff
  return false;
}
</script>
<form onsubmit="return submitHandler()">
```

```
vue中{{{ html }}} 可escape html
```

```
php mongo install
sudo apt-get install php5-mongodb
sudo apt-get install php5-mongo
php -i | grep mongo
sudo service php5-fpm restart
```

```
要获得商品的dept_ids，统一由解析adapi得到的product_group映射得到的dept(自定义的25个类)，
```

```
虚拟机内的所有服务，如果需要外网可以访问，需要修改其配置中的host为0.0.0.0
```

```
为目录创建软链接
rm 软链接名称 （比如datartery-amazon）
ln -s 目标目录或文件 软链接名称
```

查看所有的logger:
```python
>>> import logging
>>> logging.Logger.manager.loggerDict
```
PHP中命名规范为驼峰；
Python命名规范为蛇形（下划线）

列表表达式和枚举遍历
```python
>>> [i for i in range(10) if i % 2 == 0 ]
[0, 2, 4, 6, 8]
>>> nums = [2, 4, 6, 8]
>>> for i, num in enumerate(nums)
>>>    print i, num
```

迭代器（实现迭代器协议的容器对象）满足条件：
1. next 返回下一个值
2. __iter__ 返回迭代器本身

```
>>> it = iter('abc')
>>> for i in it:
>>>    print i
a
b
c
```

yield 暂停一个函数并返回中间结果。
```python
>>> def fibonacci():
>>>     a, b = 0, 1
>>>     while True:
>>>         yield b
>>>         a, b = b, a+b
>>> f = fibonacci()  # 返回一个迭代器, generator对象
>>> f.next()
```
??? tokenize

下面的yield是一个表达式，其值可以通过send函数传入。
```python
>>> def foo():
>>>     print 'input something'
>>>     while True:
>>>         v = (yield)
>>>         print v
>>> f = foo()
>>> f.next()
input something
>>> f.send('hello')
hello
```

php 时间转化
```python
$new_date_format = date('Y-m-d H:i:s', strtotime('2008-07-01T22:35:17.02'));
```

leecode 问题
[3sum](https://leetcode.com/problems/3sum/)
```python
    S = [-1, 0, 1, 2, -1, -4]
    s = sorted(S)
    result = []
    for i, n in enumerate(s):
        for k in range(i + 1, len(s)):
            p = s[k]
            r = - (n + p)
            temp = (n, p, r)
            if r in s[k + 1:] and temp not in result:
               result.append(temp)

    print result
```
