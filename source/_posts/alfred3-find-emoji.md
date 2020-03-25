title: Alfred3-Find-emoji
url: 15188.html
id: 15188
categories:
  - Computer
  - Python
tags: []

cover: /images/pasted-17.png
date: 2020-02-29 20:55:17
---
今天写了一个Alfred的workflow，简单记一下遇到的问题。 

![upload successful](/images/pasted-17.png) 
首先，如果使用python开发Alfred最好使用python2，目前还没有找到支持python3版本的库。 如果使用python2就可以使用 [Alfred-Workflow](https://www.deanishe.net/alfred-workflow/index.html)
这个库，很方便而且提供了很多API可以直接调用。
<!-- more -->
```python
    def main(wf):
         wf.send_feedback()
    if __name__ == '__main__':
        wf = Workflow()  
        log = wf.logger
        wf.run(main)
```

从Workflow() 实例化开始，任务执行正式开始。

wf传入是实例，传入的参数在wf中，如果需要获取传入的参数可以通过wf.args获取
```python
    args = wf.args
    input_data = args[0]
```
之后，由于是workflow很可能会遇到搜索数据的场景。这个库提供了一个方法来过滤数据
```py
    tmp = wf.filter(input_data, data.keys(), key=lambda x: x)
```
此外，如果需要发布程序，需要把[Alfred-Workflow](https://www.deanishe.net/alfred-workflow/index.html)本地化，可以新建一个文件夹来放这个库。 

![upload successful](/images/pasted-18.png) 

回到这个项目本身，这个项目中，所有数据都存贮在json中，所以我们可以直接搜索键值来定位数据。

![upload successful](/images/pasted-19.png)
