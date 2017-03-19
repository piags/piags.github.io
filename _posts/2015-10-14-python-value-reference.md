---
layout: post
category : python
tags : [python, function parameter, value, reference]
title: Python 函数参数传递：传值? 引用?
---

原文出自[winterTTr的CSDN](http://blog.csdn.net/muzilanlan/article/details/45645285)


在开始之前，有必要分清一下python的一些基础概念。
首先要说的是：*变量* 与 *对象* 
	
> 1. 在python中，类型属于对象，变量是没有类型的，这正是python的语言特性，也是吸引着很多pythoner的一点。所有的变量都可以理解是内存中一个对象的“引用”。或者，也可以看似c中void\*的感觉。所以，希望大家在看到一个python变量的时候，把变量和真正的内存对象分开。
> 2. 类型是属于对象的，而不是变量。这样，很多问题就容易思考了。

例如： 
{% highlight python %}
nfoo = 1   #一个指向int数据类型的nfoo（再次提醒，nfoo没有类型）
lstFoo = [1]   #一个指向list类型的lstFoo，这个list中包含一个整数1。
{% endhighlight %}
对应于上一个概念，就必须引出另了另一概念，这就是“可更改”（mutable）与“不可更改”（immutable）对象。
对于python比较熟悉的人们都应该了解这个事实，在python中，strings、tuples和numbers是不可更改的对象，而list和dict等则是可以修改的对象。那么，这些所谓的可改变和不可改变影响着什么呢？
还是上面的例子：
`nfoo = 2`
这时，内存中原始的1对象因为不能改变，于是被“抛弃”，nfoo指向一个新的int对象，其值为2。
`lstFoo[0] = 2`
更改list中第一个元素的值，因为list是可改变的，所以，第一个元素变更为2，其实应该说有一个新int对象被指定给lstFoo所指向的对象的第一个值，但是对于lstFoo来说，所指向的对象，并没有变化，就是这个看似void\*的变量所指向的对象仍旧是刚刚的那个有一个int对象的list。
好了，转回题目的问题，Python的函数参数传递：传值？引用？
对于变量（与对象相对的概念），其实，python函数参数传递可以理解为就是`变量`传值操作 \\
接着说例子好了：
{% highlight python %}
def ChangeInt(a):
      a = 10  # change the number
nfoo = 2 
ChangeInt(nfoo)
print nfoo #结果是2
{% endhighlight %}
这时发生了什么，有一个int对象2，和指向它的变量nfoo，当传递给ChangeInt的时候，按照传值的方式，复制了变量nfoo的值，这样，a就是nfoo指向同一个Int对象了，函数中a=10的时候，发生什么？
（还记得我上面讲到的那些概念么），int是不能更改的对象，于是，做了一个新的int对象，另a指向它（但是此时，被变量nfoo指向的对象，没有发生变化），于是在外面的感觉就是函数没有改变nfoo的值，看起来像C++中的传值方式。
{% highlight python %}
def ChangeList(a):
      a[0] = 10  # change the number
lstFoo = [2]
ChangeList(lstFoo)
print nfoo #结果是[10]
{% endhighlight %}
当传递给ChangeList的时候，变量仍旧按照“传值”的方式，复制了变量lstFoo的值，于是a和lstFoo指向同一个对象。但是，list是可以改变的对象，对a的操作，就是对lstFoo指向的对象的内容的操作。于是，这时的a[0] = 10，就是更改了lstFoo指向的对象的第一个元素。所以，再次输出lstFoo时，显示[10]，内容被改变了。