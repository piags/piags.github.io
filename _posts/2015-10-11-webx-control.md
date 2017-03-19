---
layout: post
category : webx
tags : [webx3, control, vm]
title: Webx中的vm中引入control的两种方式
---
###  {{page.title}}

#### 关于Webx的vm中引入control的两种方式：$control.setTemplate()与#parse()的区别

webx的vm模板分为screen展现页面的主题部分，layout用于系统的布局和结构，control用于承载系统中共用的部分；

webx中既可以通过#parse()引用control，也可以通过$control.setTemplate()引用；

* \#parse()是velocity层面的引用，father.vm通过#parse(son.vm)引用了son.vm模板之后，可以理解为son.vm是father.vm的一部分，son.vm如果有对应后端处理逻辑，是不会被执行的，但是son.vm中可以共用father.vm的参数变量；
* $control.setTemplate()是webx层面提供的一种control引用方式，father.vm通过$control.setTemplate(son.vm)引用了son.vm之后，father.vm会进行顺序解析，在解析到$control.setTemplate()的时候，会进行到son.vm模板中去进行解析，所以会执行son.vm所对应的后端处理逻辑；同时，son.vm中不能使用father.vm中的参数，如果需要将father.vm中的变量共享到son.vm，可以通过setParameter()传入son.vm中。

简而言之：

1. \#parse()是velocity层面，$control.setTemplate()是webx层面
2. \#parse()不会执行引用vm的后端逻辑，$control.setTemplate()会执行
3. \#parse()引用vm与被引用vm共享参数变量集，$control.setTemplate()如需共享，需要传入