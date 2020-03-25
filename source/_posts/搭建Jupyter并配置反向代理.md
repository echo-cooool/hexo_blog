title: 搭建Jupyter并配置反向代理
tags: []
categories: []
cover: /images/pasted-33.png

date: 2019-04-05 16:43:36
---
## 一、搭建Jupyter

### 1.安装


使用virtualenv建虚拟环境。在虚拟环境中安装jupyter、matplotlib等等需要的库。这里不赘述了。 ### 2.配置
<!-- more -->
为Jupyter 相关文件准备一个目录
```shell
mkdir /data/jupyter
cd /data/jupyter

```

建立一个目录作为 Jupyter 运行的根目录 

```shell
mkdir /data/jupyter/root
```

我们以需要密码验证的模式启动 Jupyter，所以要预先生成所需的密码对应的密文。 使用下面的命令创建一个密文的密码 python2
```shell
python -c "import IPython;print IPython.lib.passwd()"

```

python3
```shell
python -c "import IPython;print(IPython.lib.passwd())"
```

执行后需要输入并确认密码，然后程序会返回一个 `'sha1:...'` 的密文，留好了，我们接下来将会用到它。 查看用户目录 `~/.jupyter` 路径下是否存`jupyter_notebook_config.py` 文件。若不存在，产生此文件。 
```shell
jupyter notebook --generate-config
```

编辑此文件，在最后写入 
```shell
c.NotebookApp.ip = '*' # 允许访问此服务器的 IP，星号表示任意 IP
c.NotebookApp.password = u'sha1:xxx:xxx' # 之前生成的密码 hash 字串
c.NotebookApp.open_browser = Fals # 运行时不打开本机浏览器
c.NotebookApp.port = 8888 # 使用的端口
c.NotebookApp.enable_mathjax = True # 启用 MathJax
```

### 3.运行

这时采用 IP:端口号 或者 域名:端口号的方式就可以访问正常使用了。 域名访问默认80端口，接下来我们使用最常用的Nginx做代理，实现直接使用域名进行访问，隐藏端口信息。先对Jupyter进行以下修改 将配置文件ip改为只有本机才能访问
```shell
c.NotebookApp.ip = '0.0.0.0' # 127.0.0.1 也可以的
```

后台运行起来
```shell
nohup jupyter notebook > /dev/null 2>&1 &
```

## 二、Nginx代理

### 1.安装与设置

```shell
apt-get install nginx
```

### 2.查看版本

```shell
nginx -v

```

### 3.启动停止

安装完成后，使用 `nginx` 命令就可以直接启动 Nginx 

```shell
$ nginx

```

也可以使用服务器
```shell
$ service nginx start
$ service nginx stop
$ service nginx restart
```

访问 http://YOUR_IP 或者 域名 就可以看到Nginx的测试页面。 

### 4.配置

配置文件在nginx目录下，nginx.conf文件中可以看到代理的部分在在这里 `/etc/nginx/sites-enabled/defalut`。

```shell
$ sudo vim /etc/nginx/sites-enabled/defalut
```

修改其中的 location / 部分。 
```shell
server {
    server_name DOMAIN IP_ADDRESS; # 服务器域名和 IP 地址
    listen 80;
    ...
    ...
    location / {
        proxy_pass http://127.0.0.1:YOUR_PORT
    }
}
```


![](http://blog.echo.cool/wp-content/uploads/2019/04/搭建jupyter并配置反向代理.jpg)
按照上面的方法配置 Jupyter Notebook，如果仅仅对端口号进行代理转发，会出现 terminal 可以正常创建而 notebook 无法正常创建或者使用的情况。
因为 Jupyter 会对 http 请求进行判断，所以反向代理时需要设置正确的信息。正确配置 nginx 反向代理的方式如下：

```shell
server {
    server_name DOMAIN IP_ADDRESS; # 服务器域名和 IP 地址
    listen 80;
    ...
    ...
    location / {
        proxy_pass http://127.0.0.1:YOUR_PORT/;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_redirect off;
    }
}

```

重启Nginx服务让设置生效。 
```shell
$ sudo nginx -s reload

```

一切正常，晚上吃鸡！不不不，开始干活!

![upload successful](/images/pasted-16.png)


### 5.可选 

目前的URL为 `http://dyan.club/tree?`，可以在 `jupyter_notebook_config.py` 中增加 `base_url` 作为url的路径，来表示服务器上的Jupyter目录的地址。更新后的地址为 `http://dyan.club/ipython/tree?`。 
```shell
c.NotebookApp.base_url = '/ipython/'
--制定url的path,默认是根目录

```

目前没有启用ssl，安全性不够，也可以增加ssl协议增强安全性。