查看所有的logger:
```
>>> import logging
>>> logging.Logger.manager.loggerDict
```
PHP中命名规范为驼峰；
Python命名规范为蛇形（下划线）

列表表达式和枚举遍历
```
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
```
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
```
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
```
$old_date = date('l, F d y h:i:s');              // returns Saturday, January 30 10 02:06:34
$old_date_timestamp = strtotime($old_date);
$new_date = date('Y-m-d H:i:s', $old_date_timestamp); 
```
