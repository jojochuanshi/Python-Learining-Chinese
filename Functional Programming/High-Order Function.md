# 高阶函数

```
functional programming 的一个特点就是，允许函数本身作为一个参数传入另外一个函数，还允许返回一个函数。
```

```
Python 本身不是纯函数式编程语言，因为其允许使用变量。
```

- **函数本身也可以赋值给变量**
   ```python
  >>> f = abs
  >>> f(-10)
  10
  ```

**高阶函数就是让函数的参数可以接受别的函数，即别的函数可以作为另一个函数的参数**

## map/reduce函数
**map()和reduce()都是python的内置函数**
[Google相关论文](https://research.google/pubs/pub62/)

### map()函数
该函数接受两个参数，一个是函数，一个是`Iterable`，map函数将传入的函数依次作用在序列的每个元素上，并把结果作为新的`Iterable`返回。

例子：
```Python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```
上述例子中，参数f为函数，后面的list即是`Iterable`。

### reduce函数
`reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)`

该函数是将一个函数作用在一个序列上，这个函数必须接受两个参数，`reduce函数`把结果继续和序列中的下一个元素做累积计算：

**序列求和**
 ```Python
 >>> from functools import reduce
 >>> def add(x, y):
 ...     return x + y
 ...
 >>> reduce(add, [1, 3, 5, 7, 9])
 25
```

## filter
**该函数用于过滤序列**

**和`map函数`类似，`filter函数`也接受一个函数和一个序列，不同的是，`filter函数`将传入的函数依次作用于每个元素，然后根据返回值是`True`或`False`决定是否保留。**

1.list中保留奇数：
```Python
def is_odd(n):
    return n % 2 == 1

list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
```

2.list中删除空字符串
```python
def not_empty(s):
    return s and s.strip()

list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
```


## sorted 函数

1.sorted()哈数可以对list进行排序：
```Python
>>> sorted([36, 5, -12, 9, -21])
[-21, -12, 5, 9, 36]
```

2.接受`key`函数来实现自定义排序
```Python
>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]
```

**上面例子是按照绝对值大小进行排序的。**

3.sorted函数也可以对字符串进行排序

**默认情况下，对字符串排序安札ASCII大小进行比较**

4.要进行反向排序，不必改动key函数，可以传入第三个参数reverse=True
```Python
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
['Zoo', 'Credit', 'bob', 'about']
```
