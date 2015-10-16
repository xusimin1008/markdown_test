# [collections](https://docs.python.org/2/library/collections.html) #

### [Counter](http://code.activestate.com/recipes/576611/) ###

A Counter is a dict subclass for counting hashable objects. 

It is an unordered collection where elements are stored as dictionary keys and their counts are stored as dictionary values. 

说明对dict可以使用的方法对Counter也可以使用。

初始化：

counter = Counter([iterable-or-mapping]) 

```
>>> c = Counter()                           # a new, empty counter
>>> c = Counter('gallahad')                 # a new counter from an iterable
>>> c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
>>> c = Counter(cats=4, dogs=8)             # a new counter from keyword args
```

对于不存在的键，则返回0.
```
>>> c = Counter(['eggs', 'ham'])
>>> c['bacon']                              # count of a missing element is zero
0
```

#### 主要方法：###

**elements()**

*If an element’s count is less than one, elements() will ignore it.*
```
>>> c = Counter(a=4, b=2, c=0, d=-2)
>>> list(c.elements())
['a', 'a', 'a', 'a', 'b', 'b']
```

**most_common([n])**

*If n is omitted or None, most_common() returns all elements in the counter. *
```
>>> Counter('abracadabra').most_common(3)
[('a', 5), ('r', 2), ('b', 2)]
```

**subtract([iterable-or-mapping])**

```
>>> c = Counter(a=4, b=2, c=0, d=-2)
>>> d = Counter(a=1, b=2, c=3, d=4)
>>> c.subtract(d)
>>> c
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```

** update([iterable-or-mapping]) **
Like dict.update() but adds counts instead of replacing them. 

_相当于add方法_
```
>>> c = Counter(a=4, b=2, c=0, d=-2)
>>> d = Counter(a=1, b=2, c=3, d=4, e=-4)
Counter({'a': 5, 'b': 4, 'c': 3, 'd': 2, 'e': -4})
```

Several mathematical operations are provided for combining Counter objects to produce multisets 

(counters that have counts greater than zero). 
```
c += Counter()                  # remove zero and negative counts

>>> c = Counter(a=3, b=1)
>>> d = Counter(a=1, b=2)
>>> c + d                       # add two counters together:  c[x] + d[x]
Counter({'a': 4, 'b': 3})
>>> c - d                       # subtract (keeping only positive counts)
Counter({'a': 2})
>>> c & d                       # intersection:  min(c[x], d[x])
Counter({'a': 1, 'b': 1})
>>> c | d                       # union:  max(c[x], d[x])
Counter({'a': 3, 'b': 2})
```

***

