---
title: 使用Python解析JSON格式数据
tags:
  - json
  - python
url: 14334.html
id: 14334
categories:
  - Computer
  - Python
date: 2018-05-25 18:31:50
---

JSON是一种轻量级的数据交换格式。在很多场合，我们都需要用到JSON。在Python语言中，我们使用json模块，来编码和解码JSON格式的数据。其中两个主要的函数是 json.dumps() 和 json.loads() ，下面演示如何将一个Python数据结构转换为JSON： json.dumps() json.dumps()方法，可以用来将Python数据结构转换为JSON数据格式。

import json

data = {

'name':'python',

'age': '20',

'sex':'male'

}



json_str = json.dumps(data)

print(json_str)

运行上面这个程序后，将输出以下内容：

 

{"name": "python", "age": "20", "sex": "male"}

输出的内容，就是一个json字符串。 如何将一个JSON编码的字符串转换回一个Python数据结构：

py\_data = json.loads(json\_str)

print(py_data)

print(type(py_data))

  运行上面的程序后，你会看到如下的输出：  

{'name': 'python', 'age': '20', 'sex': 'male'}

<class 'dict'>

  这里输出的其实是python的字典。我们将一个JSON格式数据，转换为python语言的的字典格式。   编码和解码JSON数据文件 如果我们处理的JSON数据，不是一个字符串，而是放在文件中，该怎么处理呢？下面演示如何处理JSON文件：   # 写入一个json格式数据到data.json文件中

with open('data.json', 'w') as f:

json.dump(data, f)

  # 将文件中的json数据，读取出来，解码为字典 with open('data.json', 'r') as f: data = json.load(f) **小结** JSON编码的格式对于Python语法而已几乎是完全一样的，除了一些小的差异之外。 比如，True会被映射为true，False被映射为false，而None会被映射为null。这里我只介绍了json.dumps和json.loads、json.load、json.load这4个方法，其实它还有更多方法。json 模块还有很多其他选项来控制更低级别的数字、特殊值如NaN等的解析。 可以参考官方文档获取更多细节。