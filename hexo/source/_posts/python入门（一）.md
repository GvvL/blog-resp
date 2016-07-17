---
title: python入门(一)
date: 2016-06-07 15:44:07
categories: python
tags:
    - python
    - 函数
    - 变量
    - 装饰器
    - 垃圾回收
    - 偏函数

---
## 变量
    python数据类型没有值类型，全部为引用类型。所以变量的类型即是其指向的内存中的对象类型。对象则分为两类:可修改与不可修改的。
    可变类型包括，字典、列表、集合和类实例等对象。
## 函数
### 函数参数
    在Python中定义函数，可以用必选参数、默认参数、可变参数和关键字参数，这4种参数都可以一起使用，或者只用其中某些，但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数和关键字参数。
    
    比如定义一个函数，包含上述4种参数：
    
``` bash
def func(a, b, c=0, *args, **kw):
    print 'a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw
``` 
    在函数调用的时候，Python解释器自动按照参数位置和参数名把对应的参数传进去。
``` bash
>>> func(1, 2)
a = 1 b = 2 c = 0 args = () kw = {}
>>> func(1, 2, c=3)
a = 1 b = 2 c = 3 args = () kw = {}
>>> func(1, 2, 3, 'a', 'b')
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}
>>> func(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
```
    还可以将args传入一个元组，kw传入一个字典
``` bash
>>> args = (1, 2, 3, 4)
>>> kw = {'x': 99}
>>> func(*args, **kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'x': 99}
```
### 匿名函数
只可以有一个表达式：
如：

``` bash
map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9])
#还可以作为返回值
def build(x, y):
    return lambda: x * x + y * y
```
    
## 高级特性
---
### 切片
``` bash
l=range(100)
l[-10:]#取倒数
l[10:30:3]#取10到30步长为3
s=l[:]#数组拷贝
```
tips:不仅数组，所有实现了__getitem__方法的对象都可以进行切片，例如 str，tuple
### 迭代
for in 循环，若要实现类java式的下标循环，需使用enumerate函数对其进行转换
``` bash
>>> for i, value in enumerate(['A', 'B', 'C']):
         print i, value
```
类同切片所有实现了__iter__的对象都可迭代
### 排序sort
sorted(list,f) f为接受连个参数返回1，-1,0的方法 

### 装饰器

``` bash
import functools

def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print 'call %s():' % func.__name__
        return func(*args, **kw)
    return wrapper
#或者如下
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print '%s %s():' % (text, func.__name__)
            return func(*args, **kw)
        return wrapper
    return decorator
```   

### 偏函数
固定现有函数的一些参数，生成一个新函数,functools.partial(原函数名称, **kw):

``` bash
import functools
int2 = functools.partial(int, base=2)
max2 = functools.partial(max, 10)
```
像max2如果不指定形参名称，或形参名称不存在，则自动将改kw追加到函数参数的第一个位置
``` bash
max2(5, 6, 7)
#相当于
args = (10, 5, 6, 7)
max(*args)
```

## 垃圾回收
    python垃圾回收机制是引用计数。当一个对象的引用数目为0的时候，才会被从内存中回收。避免循环强引用可使用weakref
    
