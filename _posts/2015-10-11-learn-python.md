---
layout: post
category : python
tags : [python]
title: Python 学习笔记
---

#### Python命令行参数sys.argv

命令行参数是通过sys.argv[]来获取的，sys.argv[0]是代码文件本身的路径，因此参数是从1开始的。比如设置参数为: spe \\
Python代码：

```python
import os, sys
os.system(sys.argv[1])
```

带参数执行 ```python xxx.py spe```
os.system 是用来执行命令行的。因此该程序会接收到第一个参数spe，然后在命令行里执行spe，这样，spe（Python IDE）就打开了。


#### Python字符串字串查找 find和index方法
Python字符串查找有4个方法: find、index、rfind和rindex。

* find()方法: 查找子字符串，若找到返回从0开始的下标值，若找不到返回-1

```python
info = 'abca'
print info.find('a')##从下标0开始，查找在字符串里第一个出现的子串，返回结果：0

info = 'abca'
print info.find('a',1)##从下标1开始，查找在字符串里第一个出现的子串：返回结果3

info = 'abca'
print info.find('333')##返回-1,查找不到返回-1
```

* index()方法: 在字符串里查找子串第一次出现的位置，类似字符串的find方法，不过比find方法更好的是，如果查找不到子串，会抛出异常，而不是返回-1

```python
info = 'abca'
print info.index('a')
print info.index('33')
```

rfind和rindex方法用法和上面一样，只是从字符串的末尾开始查找。


#### Python过滤中文、英文标点特殊符号

转自[这里](http://blog.csdn.net/mach_learn/article/details/41744487)

下面是一封垃圾邮件的过滤实例：\\
"想做/ 兼_职/学生_/ 的 、加,我Q：  1 5.  8 0. ！！？？  8 6 。0.  2。 3     有,惊,喜,哦" \\
邮件中的“！？。、”都是中文的，而“/.”是英文的 \\
下面是过滤方式：

```python
#-*-coding:utf-8-*-  
import re  
temp = "想做/ 兼_职/学生_/ 的 、加,我Q：  1 5.  8 0. ！！？？  8 6 。0.  2。 3     有,惊,喜,哦"  
temp = temp.decode("utf8")  
string = re.sub("[\s+\.\!\/_,$%^*(+\"\']+|[+——！，。？、~@#￥%……&*（）]+".decode("utf8"), "".decode("utf8"), temp)  
print string  
```

Python通过re模块提供对正则表达式的支持，re是regular expression的所写，表示正则表达式，sub是substitute的所写，表示替换；re.sub是个正则表达式方面的函数，用来实现通过正则表达式，实现比普通字符串的replace更加强大的替换功能；\\ 
re.sub共有五个参数。其中三个必选参数：pattern, repl, string，两个可选参数：count, flags。\\
详细见[这里](http://www.crifan.com/python_re_sub_detailed_introduction/comment-page-1/)

#### Python获得字符的ASCII码，将ASCII数字转换为字符

下面的代码可以在字符和ascii码之间互转。

```python
# Get the ASCII number of a character
number = ord(char)
# Get the character given by an ASCII number
char = chr(number)
```
如果是Unicode字符，可以使用ord()和unichr()函数。

#### Python中删除字符串连续的空格，只保留一个空格
不区分tab的话，可以使用```' '.join(s.split())```


#### 字符或字符串内容类型判断

```python
# s为字符串
s.isalnum() # 所有字符都是数字或者字母
s.isalpha() # 所有字符都是字母
s.isdigit() # 所有字符都是数字
s.islower() # 所有字符都是小写
s.isupper() # 所有字符都是大写
s.istitle() # 所有单词都是首字母大写，像标题
s.isspace() # 所有字符都是空白字符、\t、\n、\r
```

#### 目录操作

```python
import os 
if os.path.isdir('E:\test'): # 判断目录是否存在 
	pass 
else: 
	os.mkdir('E:\test') # 新建目录
```

#### 集合遍历

```python
# 遍历list
info = ['a','b','c','d']
for i in info:
	print i

# 遍历dictionary
dict={"name":"mike","age":20,"gender":'male'}
for i in dict:
	print "dict[%s]=" % i,dict[i]
```

#### 字典dictionary相关
##### 字典中的值是列表

```python
# 语法
dic = {}
dic.setdefault(key, []).append(value)
```

##### 按键和值排序
按值（value）排序

```python
dic = {'a':31, 'bc':5, 'c':3, 'asd':4, 'aa':74, 'd':0}
dict= sorted(dic.iteritems(), key=lambda d:d[1], reverse = True)
print dict
```
输出的结果：
[('aa', 74), ('a', 31), ('bc', 5), ('asd', 4), ('c', 3), ('d', 0)]
注意，输出是列表。

下面我们分解下代码
dic.iteritems() 得到[(键，值)]的列表。
然后用sorted方法，通过key这个参数，指定排序是按照value，也就是第一个元素d[1]的值来排序。reverse = True表示是需要翻转的，默认是从小到大，翻转的话，那就是从大到小。

按键（key）排序

```python
dic = {'a':31, 'bc':5, 'c':3, 'asd':4, 'aa':74, 'd':0}
dict= sorted(dic.iteritems(), key=lambda d:d[0]) #d[0]表示字典的键
print dict
```
区别在于指定排序的参数```key=lambda d:d[0]```。

#### 自动给数字前面补0的方法
str的zfill方法用来给字符串前面补0，非常有用

```python
n = "123"
s = n.zfill(5)
assert s == "00123"

#zfill()也可以给负数补0
n = "-123"
s = n.zfill(5)
assert s == "-0123"

#对于纯数字，我们也可以通过格式化的方式来补0
n = 123
s = "%05d" % n
assert s == "00123"
```
