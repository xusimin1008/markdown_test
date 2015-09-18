# Python Json #
## 为什么选择Json ##
我们把变量从内存中变成可存储或传输的过程称之为序列化。
序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上，
反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化。

一般的Python序列化，pickle只能用于Python，并且可能不同版本的Python彼此都不兼容,
我们要在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如XML，但更好的方法是序列化为JSON，它比XML更快， 
所以我们选择Json。

## Python数据类型与Json数据类型的对应 ##
        JSON类型	     Python类型
        {}	         dict
        []	         list
        "string"	 'str'或u'unicode'
        1234.56	     int或float
        true/false	 True/False
        null	     None


## 序列化操作 ##

`json.dumps()` 序列化
`json.loads()` 反序列化，_得到的所有字符串对象默认都是unicode而不是str_。

正常情况下，类的序列化是会报错的，
那么如何把类序列化？
假设有个学生Student类，

        class Student(object):
            def __init__(self, name, age, score):
                self.name = name
                self.age = age
                self.score = score

在类里面写一个转化函数，之后传入dumps()里，

        def student2dict(std):
            return {
                'name': std.name,
                'age': std.age,
                'score': std.score
            }

        print(json.dumps(s, default=student2dict))

如何反序列化？
在类里面写一个转化函数，之后传入loads()里，

        def dict2student(d):
            return Student(d['name'], d['age'], d['score'])


## 几个不同json库的比较 ##          

cjson是用C语言实现，

yajl是Cython版本的JSON实现。 

simplejson与标准库JSON的区别不大，但更新可能更快。


python 对象序列化

[序列化](http://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/00138683221577998e407bb309542d9b6a68d9276bc3dbe000)

[Python 对象序列化——pickle and cPickle](http://segmentfault.com/a/1190000000641920)

[Python序列化](http://beginman.cn/python/2015/05/19/Python-cc/)

[Python序列化的两种方式进行比较（pickle和json的比较）](http://www.huangxiaohao.com/2015/08/python%E5%BA%8F%E5%88%97%E5%8C%96%E7%9A%84%E4%B8%A4%E7%A7%8D%E6%96%B9%E5%BC%8F%E8%BF%9B%E8%A1%8C%E6%AF%94%E8%BE%83%EF%BC%88pickle%E5%92%8Cjson%E7%9A%84%E6%AF%94%E8%BE%83%EF%BC%89/)

[编写高质量Python代码（3）——库](http://www.wengweitao.com/bian-xie-gao-zhi-liang-pythondai-ma-3-ku.html)

[读写JSON数据](http://python3-cookbook.readthedocs.org/zh_CN/latest/c06/p02_read-write_json_data.html)

http://simplejson.readthedocs.org/en/latest/

http://docs.python-guide.org/en/latest/scenarios/json/

[anyjson](https://pypi.python.org/pypi/anyjson/0.3.3)
