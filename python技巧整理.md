Python技巧整理
==
-----

###通过简单的运行你就可以监控Python代码:
    python -m cProfile myprogram.py

-----
###同步python环境 安装:
	pip freeze > requirements.txt
	pip install -r requirements.txt

-----
###取当前工作目录:
	import os  # 确定使用import os风格而不是from os import *。这将避免os.open()被内建的open()函数遮住，它的操作截然不同。
	os.getcwd()

-----
###glob模块提供了一个函数可以从目录通配符搜索获得文件列表：

	import glob
	glob.glob('*.py')

-----
###数据压缩

	import zlib
	zlib.compress(s)  # 压缩
	zlib.decompress(s)  # 解缩

-----
###装饰器的作用就是为已经存在的对象添加额外的功能。
-----
###计数时使用Counter 计数对象。
这听起来显而易见，但经常被人忘记。对于大多数程序员来说，数一个东西是一项很常见的任务，而且在大多数情况下并不是很有挑战性的事情——这里有几种方法能更简单的完成这种任务。  
Python的collections 类库里有个内置的dict类的子类，是专门来干这种事情的：


	>>> from collections import Counter
	>>> Counter('hello world')
	Counter({'l': 3, 'o': 2, ' ': 1, 'e': 1, 'd': 1, 'h': 1, 'r': 1, 'w': 1})

-----
####内置函数:

	cmp(2.3, 3.2)                    # 比较两个数的大小
	divmod(9,2)                      # 返回除法结果和余数
	slice(5,2,-1)                    # 构建下标对象 slice
	all([True, 1, "hello!"])         # 是否所有的元素都相当于True值
	any(["", 0, False, [], None])    # 是否有任意一个元素相当于True值
	reversed([1,5,3])                # 返回反序的序列，也就是[3,5,1]

-----
####迭代器
[Link](evernote:///view/3290116/s29/41a0222d-1a48-46fa-9560-36ace06db9d0/41a0222d-1a48-46fa-9560-36ace06db9d0/)

-----
####索引 & 项enumerate:
	for (index, item) in enumerate(items):  
		print index, item  

-----
####python 的几个内置函数（lambda ,zip, filter, map, reduce ）用法
zip  zip函数接受任意多个序列作为参数，将所有序列按相同的索引组合成一个元素是各个序列合并成的tuple的新序列，新的序列的长度以参数中最短的序列为准。另外(*)操作符与zip函数配合可以实现与zip相反的功能，即将合并的序列拆成多个tuple

	>>>x=[1,2,3],y=['a','b','c']
	>>>zip(x,y)
	[(1,'a'),(2,'b'),(3,'c')]
	>>>zip(*zip(x,y))
	[(1,2,3),('a','b','c')]

-----
####map为操作list,返回list,绑定的函数为修改list中每一个值的函数

	>>> list=[1,2,3]
	>>> map(lambda x : x*2,list)
	>>> [2, 4, 6]

-----
####reduce为逐次操作list里的每项，接收的参数为 2个,最后返回的为一个结果

	>>> def myadd(x,y):  
	>>> 	return x+y
	>>> sum = reduce(myadd,(1,2,3)) 
	>>> 6

-----
####漂亮地print数据

	print json.dumps(s, indent=2)

-----
####字典排序

	from operator import itemgetter
	sorted(d.iteritems(), key=itemgetter(1), reverse=True)

-----
####locals()直接使用当前上下文中的变量

	name, age = 'Mar', 18
	print 'Hello, %(name)s . Are you %(age)d?' % locals()

-----
####字符串 相似度 找不同
[difflib](http://docs.python.org/2/library/difflib.html)

	>>> import difflib
	>>> difflib.SequenceMatcher(None, 'abcde', 'abcde').ratio()
	1.0
	>>> difflib.SequenceMatcher(None, 'abcde', 'zbcde').ratio()
	0.80000000000000004
	>>> difflib.SequenceMatcher(None, 'abcde', 'zyzzy').ratio()
	0.0

-----
####Python 变量 存储为 字符串
	import base64
	import pickle
	#写
	w = lambda s: base64.encodestring(pickle.dumps(s))
	#读
	r = lambda s: pickle.loads(base64.decodestring(s))

-------------
####shelve — Python对象持久性

	import shelve
	db = shelve.open(LastUpdated, writeback = True)
	db['abc'] = 123

-------------
####函数式编程
	>>> def make_incrementor (n): return lambda x: x + n
	>>> 
	>>> f = make_incrementor(2)
	>>> g = make_incrementor(6)
	>>> 
	>>> print f(42), g(42)
	44 48
	>>> 
	>>> print make_incrementor(22)(33)
	55

-------------
#### 短路机制

	if a:
	    print a
	else
	    print b
	# 可以写成
	print a or b

-------------
###dict.setdefault()
如果 key 在 dict 中，回傳 value 值，反之，將 key:default 加入 dict 之中。

----------
###断言语句

	assert age >= 12

------------
###repr()  # 把返回字符串的表现形式 展现出来 
---------
###拆子列表
方法一:

	a= [(0, 0), (0, 0), (0, 15), (0, 16), (0, 13)]
	reduce(lambda a, b: a | b, a)

方法二:

	>>> nested = [[1, 2, 3], [4, 5], [6, 7, 8]]
	>>> [number for inner in nested if len(inner) > 2 for number in inner]
	[1, 2, 3, 6, 7, 8]

方法三:

	from itertools import chain
	chain('ABC', 'DEF') --> A B C D E F

---
###iter()可接收callable参数

iter()内建函数接收的参数分为两种，第一种是：

iter(collection)---> iterator
参数collection必须是可迭代对象或者是序列 ，第二种是：

iter（callable， sentinel) --> iterator
callable函数会一直被调用，直到它的返回结果等于sentinel，例如：

	def seek_next_line(f):
	    #每次读一个字符，直到出现换行符就返回
	    for c in iter(lambda: f.read(1),'\n'):
	        pass

---
###Python列表推导的四个技巧
多级循环

	>>> nested = [[1, 2, 3], [4, 5], [6, 7, 8]]
	>>> [number for inner in nested if len(inner) > 2 for number in inner]
	[1, 2, 3, 6, 7, 8]

矩阵转置：

	>>> [[i * j for j in range(1, 5)] for i in range(1, 4)]
	[[1, 2, 3, 4], [2, 4, 6, 8], [3, 6, 9, 12]]
	>>> [list(row) for row in zip(*matrix)]
	[[1, 2, 3], [2, 4, 6], [3, 6, 9], [4, 8, 12]]
	>>> list(map(list, zip(*matrix)))
	[[1, 2, 3], [2, 4, 6], [3, 6, 9], [4, 8, 12]]

数据分组 itertools.groupby()

	from itertools import groupby
	packages = {category: list(packages) for category, packages in groupby(worldfile, get_category)}

详细：
	>>> for k , g in groupby('AAAABBBCCDAABBB'):
			print k, list(g)
	     
	A ['A', 'A', 'A', 'A']
	B ['B', 'B', 'B']
	C ['C', 'C']
	D ['D']
	A ['A', 'A']
	B ['B', 'B', 'B']


Break

	[word[0] for word in itertools.takewhile(lambda word: word != "and", text.split())]

---
###[pyrobot](https://github.com/chriskiehl/pyrobot) 运行在 Windows 平台之上的自动化测试组件，类似Java的Robot类
---
###不要用if 做select ,用dict

	# Yes:
	foo_fn = {
	    bar: run,
	    car: jump,
	    jar: hide,
	    ...
	}
	
	foo_fn[foo]()    
	
	# No:
	if foo == bar:
	    run()
	elif foo == car:
	    jump()
	elif foo == jar:
	    hide()
	    ...
