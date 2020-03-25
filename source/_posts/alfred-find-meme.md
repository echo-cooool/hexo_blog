title: Alfred-Find-Meme
url: 15195.html
id: 15195
categories:
  - Computer
  - Python
tags: []
cover: /images/pasted-20.png

date: 2020-03-05 13:34:42
---
这是一个能通过Alfred脚本找到想要的表情包的应用

demo
====


![upload successful](/images/pasted-20.png)

<!-- more -->

实现方法
====

版本1.0
-----

本地加载表情包数据，通过以下代码查询
```python
    tmp += wf.filter(input_data, data.keys(), key=lambda x: x,max_results=20, match_on=17)
```
得到查询结果后，开一个新的线程来下载数据，同时调用wf.add_item来添加到显示窗口
```python
    def downloader(url):
        if url == "":
            return 0
        name = url.split('/')[-1]
        r = web.get(url)
        with open(name, "wb") as file:
            file.write(r.content)
    Thread(target=downloader, args=(url,)).start()
```
一开始并没有考虑性能优化，用的是本地`JSON`文件，但是这个`JSON`文件有将近30MB大小，而且有大约14万条表情包数据。导致在本地使用`workflow`来搜索的时候性能较差，每次搜索要大概一到两秒钟。

当时有一个思路就是改用数据库，可是Alfred使用`python2.7`，而且并不便于部署。同时Alfred脚本还要兼顾灵活性，方便传播这个脚本。所以本地数据库的方案不可行。

版本1.1
-----

调用LeanCloud REST API来查询数据，同时把所有表情包数据存入LeanCloud，并且为keyword字段添加索引来加快查询速度。 

![upload successful](/images/pasted-21.png)


![upload successful](/images/pasted-22.png)
```python
    def get_keyword(keyword):
        global api_url
        data = "where=%7B%22keyword%22%3A%7B%22%24regex%22%3A%22%5E"+keyword + \
            ".*%22%7D%7D&limit=20&&order=-updatedAt"
        api_url += "?" + data
        res = web.get(api_url, headers=header)
        return res.json()['results']
```
由于LeanCloud提供的SDK是针对`python3`的，所以我们还需要写一个查询的函数。

我用的是正则表达式匹配开头的字母，这样的好处是能利用索引加快速度，如果全部匹配的话索引就失效了。


![upload successful](/images/pasted-23.png)


这里是Alfred的框图，这里还需要解决一个问题，Alfred并没有提供复制图片到剪切板到功能。所以经过Google，我找到了一个可以在mac上使用的，把照片复制到剪贴板的程序。
```c#
    #import <Foundation/Foundation.h>
    #import <Cocoa/Cocoa.h>
    #import <unistd.h>
    BOOL copy_to_clipboard(NSString *path)
    {
      // http://stackoverflow.com/questions/2681630/how-to-read-png-image-to-nsimage
      NSImage * image;
      if([path isEqualToString:@"-"])
      {
        // http://caiustheory.com/read-standard-input-using-objective-c 
        NSFileHandle *input = [NSFileHandle fileHandleWithStandardInput];
        image = [[NSImage alloc] initWithData:[input readDataToEndOfFile]];
      }else
      { 
        image =  [[NSImage alloc] initWithContentsOfFile:path];
      }
      // http://stackoverflow.com/a/18124824/148668
      BOOL copied = false;
      if (image != nil)
      {
        NSPasteboard *pasteboard = [NSPasteboard generalPasteboard];
        [pasteboard clearContents];
        NSArray *copiedObjects = [NSArray arrayWithObject:image];
        copied = [pasteboard writeObjects:copiedObjects];
        [pasteboard release];
      }
      [image release];
      return copied;
    }
    
    int main(int argc, char * const argv[])
    {
      NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
      if(argc<2)
      {
        printf("Usage:\n\n"
          "Copy file to clipboard:\n    ./impbcopy path/to/file\n\n"
          "Copy stdin to clipboard:\n    cat /path/to/file | ./impbcopy -");
        return EXIT_FAILURE;
      }
      NSString *path= [NSString stringWithUTF8String:argv[1]];
      BOOL success = copy_to_clipboard(path);
      [pool release];
      return (success?EXIT_SUCCESS:EXIT_FAILURE);
    }
```
```
    gcc -Wall -g -O3 -ObjC -framework Foundation -framework AppKit -o impbcopy impbcopy.m
```
这样，把impbcopy放到程序目录，就可以复制了～


![upload successful](/images/pasted-24.png)


开源地址：
=====

[https://github.com/echo-cool/Alfred-Find-Meme](https://github.com/echo-cool/Alfred-Find-Meme)