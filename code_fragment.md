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
$new_date_format = date('Y-m-d H:i:s', strtotime('2008-07-01T22:35:17.02'));
```

leecode 问题
[3sum](https://leetcode.com/problems/3sum/)
```
S = [-1, 0, 1, 2, -1, -4]
    s = sorted(S)
    result = []
    for i, n in enumerate(s):
        for k in range(i + 1, len(s)):
            p = s[k]
            r = - (n + p)
            temp = (n, p, r)
            if r in s[k + 1:] and not temp in result:
               result.append(temp)

    print result
```
