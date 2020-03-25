---
title: Jupyter notebook基础使用
tags:
  - Jupyter notebook
url: 14336.html
id: 14336
categories:
  - Python
date: 2018-05-25 19:55:09
---

作者：猴子 链接：https://www.zhihu.com/question/46309360/answer/254638807 来源：知乎 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

**1.Jupyter notebook 是什么？** **2.如何安装 Jupyter notebook？** **3.如何启动Jupyter notebook？** **4.新手如何快速使用notebook？** **1.Jupyter notebook 是什么？** 在没有notebook之前，在IT领域工作的我都是这样工作的： 在普通的 Python shell 或者在IDE（集成开发环境）如Pycharm中写代码，然后在word中写文档来说明你的项目。 这个过程很反锁，通常是写完代码，再写文档的时候我还的重头回顾一遍代码。最蛋疼的地方在于，有些数据分析的中间结果，我还的重新跑代码，然后把结果弄到文档里给客户看。 有了notebook之后，我的世界突然美好了许多，因为notebook 可以直接在代码旁写出叙述性文档，而不是另外编写单独的文档。也就是它可以能将代码、文档等这一切集中到一处，让用户一目了然。 例如，我的数据分析社群小伙伴就用Jupyter notebook写出了他的学习笔记，长这样，是不是很酷：

<img class="size-full wp-image-14348" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用.jpg" width="688" height="401" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用.jpg)

所以，你现在明白了这句话是在说什么了：

> Jupyter notebook（[http://jupyter.org/](https://link.zhihu.com/?target=http%3A//jupyter.org/)） 是一种 Web 应用，能让用户将说明文本、数学方程、代码和可视化内容全部组合到一个易于共享的文档中。

<img class="size-full wp-image-14350" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-2.jpg" width="646" height="413" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-2.jpg)

**Jupyter Notebook 已迅速成为数据分析，机器学习的必备工具。因为它可以让数据分析师集中精力向用户解释整个分析过程。** Jupyter这个名字是它要服务的三种语言的缩写：Julia，PYThon和R，这个名字与“木星（jupiter）”谐音。 如果看了以上对Jupyter Notebook的介绍你还是拿不定主意究竟是否适合你，那么不要担心，你可以先**免安装试用体验**一下，[戳这里](https://link.zhihu.com/?target=https%3A//try.jupyter.org/)，然后再做决定。 值得注意的是，官方提供的同时试用是有限的，如果你点击链接之后进入的页面如下图所示，那么不要着急，过会儿再试试看吧。

<img class="size-full wp-image-14352" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-4.jpg" width="720" height="310" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-4.jpg)

试用满线

如果你足够幸运，那么你将看到如下界面，就可以开始体验啦。

<img class="size-full wp-image-14354" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-6.jpg" width="720" height="425" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-6.jpg)

主界面

<img class="size-full wp-image-14356" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-8.jpg" width="720" height="637" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-8.jpg)

<img class="size-full wp-image-14358" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-10.jpg" width="600" height="85" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-10.jpg)

**2.如何安装 Jupyter notebook？** 对于做数据分析这么有用的神器，不安装使用下是不是很遗憾？ 安装 Jupyter 的最简单方法是使用 Anaconda。该发行版附带了 Jupyter notebook。你能够在默认环境下使用 notebook。 确保你已经安装了Anaconda，如果不知道如何安装的，可以看我之前写的： conda install jupyter notebook要在 conda 环境中安装 Jupyter notebook，在conda终端使用命令（**以下所有命令是指conda的终端Anaconda Prompt**）：

<img class="size-full wp-image-14360" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-12.jpg" width="621" height="173" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-12.jpg)

也可以通过python shell的 pip 来安装：pip install jupyter notebook。

<img class="size-full wp-image-14358" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-10.jpg" width="600" height="85" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-10.jpg)

**3.如何启动Jupyter notebook？** 启动 notebook 服务器，在终端中输入： jupyter notebook。 服务器会在你运行此命令的“notebook工作文件夹”中启动。也就是说后面你操作的任何 notebook 文件都会保存在该文件夹下，类似于你用优酷下载视频，优酷都会放到自己的下载目录一样。例如我在下面的C:\\houzi 下面启动目录后，会在该目录下看到我后面运行的文件。

<img class="size-full wp-image-14364" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-16.jpg" width="617" height="128" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-16.jpg)

启动notebook 服务器后，在浏览器中打开notebook页面地址：http://localhost:8888 （其中localhost 表示你的计算机，而 8888 是服务器的默认端口）

<img class="size-full wp-image-14366" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-18.jpg" width="617" height="225" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-18.jpg)

如果你同时启动了另一个 notebook 服务器，新服务器会尝试使用端口 8888，但由于此端口已被占用，因此新服务器会在端口 8889 上运行。之后，你可以通过 http://localhost:8889 连接到新服务器。以此类推。 如果启动后遇到问题，参考这里的解决方案 **4.新手如何快速使用notebook？** **1）确保你在Anaconda终端中安装了以下包：**

*   **安装环境自动关联包**

    conda install nb_conda
    

该包可以将conda中创建的环境自动关联到你的notebook中。 我们可以对应conda中的环境，就知道这些环境对应conda中的环境列表。用 conda env list 就可以列出你创建的所有环境。

<img class="size-full wp-image-14368" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-20.jpg" width="501" height="158" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-20.jpg)

其中py2是我在conda中创建的Python2环境名称， root和default一样是默认环境，因为我安装的是Anaconda3，所以默认环境是Python3。

你会发现环境名称py3没有出现在notebook中。解决办法是按下图步骤安装包ipykernel。 （同样的，在你的py2环境下也要像刚才步骤那样安装一次这个包）

<img class="size-full wp-image-14370" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-22.jpg" width="720" height="401" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-22.jpg)

完成上面安装步骤，回到标签页“Files”，再新建notebook时，会发现已经关联了环境名称py2和py3：

<img class="size-full wp-image-14372" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-24.jpg" width="720" height="233" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-24.jpg)

这样你在notebook中可以轻松切换Python2和Python3环境了。 ps：感谢 的经验分享：经过上面步骤后，notebook的首页右上角，在新建的时候没有显示py3和py2两个环境的关联，这个时候，你可以尝试重启浏览器，注意！是重启浏览器，不是notebook！刷新浏览器有时候是没有用滴（因为缓存的原因），而然我刷了两个小时。。。

*   **在Anaconda终端安装代码自动补全包**

    conda install pyreadline
    

<img class="size-full wp-image-14374" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-26.jpg" width="668" height="274" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-26.jpg)

什么是代码自动补全呢？ 后面会介绍，您就等好吧。 **1）顶部的3个选项卡** 顶部的3个选项卡是：_Files_（文件）、_Running_（运行）和 _Cluster_（集群）。 _Files_（文件）显示当前“notebook工作文件夹”中的所有文件和文件夹。 点击 _Running_（运行）选项卡会列出所有正在运行的 notebook。可以在该选项卡中管理这些 notebook。 _Clusters一般不会用到。因为_过去在 _Clusters_（集群）中创建多个用于并行计算的内核。现在，这项工作已经由 [ipyparallel](https://link.zhihu.com/?target=https%3A//ipyparallel.readthedocs.io/en/latest/intro.html) 接管。

<img class="size-full wp-image-14376" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-28.jpg" width="620" height="233" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-28.jpg)

**2）如何创建一个新的notebook？** 像下面图片中一样，在右侧点击“New”（新建），创建新的 notebook、文本文件、文件夹或终端。 “Notebooks”下的列表显示了你已安装的内核。由于我在 Python 3 环境中运行服务器，因此列出了 Python 3 内核。你在这里看到的可能是 Python 2。这里我点击Python3。

<img class="size-full wp-image-14378" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-30.jpg" width="617" height="354" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-30.jpg)

**这样你就打开了下面的页面，你会看到外框为绿色的一个小方框。它称为_单元格_。单元格是你编写和运行代码的地方。以后你就可以在这里写你的数据分析代码了。**

<img class="size-full wp-image-14380" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-32.jpg" width="615" height="254" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-32.jpg)

在这里你可以输入自己人生中的第一行Python代码Hello world。然后点击图中的运行按钮，会执行你当前所在的代码，其实我更喜欢用快捷键（键盘上同时按住ctrl+enter键）来执行代码。

<img class="size-full wp-image-14382" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用.gif" width="695" height="392" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-34.jpg)

这句代码的意思是在界面输出字符串"Hello world！"，所以你会看到在下面与输出结果出来。 运行代码单元格时，单元格下方会显示输出。单元格还会被编号（左侧会显示 In \[1\]:）。如果运行了多个单元格的话（也就是多块代码），这能让你知道运行的代码和运行顺序。

<img class="size-full wp-image-14384" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-35.jpg" width="612" height="257" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-35.jpg)

notebook 中的大部分工作均在代码单元格中完成。这是编写和执行代码的地方。在代码单元格中可以执行多种操作，例如编写代码、给变量赋值、导入包，展示数据分析结果等。在一个单元格中执行的任何代码在所有其他单元格中均可用。 + 按钮用于创建新的单元格

<img class="size-full wp-image-14386" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-1.gif" width="695" height="493" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-37.jpg)

还记得一开始我提到代码自动补全功能吗？那么，什么是代码自动补全呢？ 比如 我定义了下面的变量。

<img class="size-full wp-image-14388" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-38.jpg" width="499" height="107" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-38.jpg)

在后面代码中用到这个变量是，我只要输入第一个变量的第一个字母p，然后按下Tab键，边会自动查找到代码中以p开头的变量名称，这可以大幅度提供你写代码的效率。 但是要注意：如果你定义的变量想出现在代码补全里，需要你先把定义该变量的cell运行以后，notebook才能识别它 当Cell前出现*，表示当前cell程序正在运行，或者它前面的cell正在运行。

<img class="size-full wp-image-14390" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-40.jpg" width="338" height="290" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-40.jpg)

作者：猴子 链接：https://www.zhihu.com/question/46309360/answer/254638807 来源：知乎 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

**2）重命名notebook** 你会看到刚才我建的notebook文件名是下面这样默认的，我想修改成自己喜欢的文件名如何办呢？

<img class="size-full wp-image-14392" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-42.jpg" width="611" height="248" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-42.jpg)

点击“File”->Rename，可以对notebook文件进行重命名，这里我命名成‘Helloworld’

<img class="size-full wp-image-14394" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-44.jpg" width="615" height="432" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-44.jpg)

<img class="size-full wp-image-14396" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-46.jpg" width="612" height="280" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-46.jpg)

<img class="size-full wp-image-14398" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-48.jpg" width="618" height="274" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-48.jpg)

同时，你可以在当前运行notebook服务器的“notebook工作文件夹”下看到创建的notebook，文件名后缀是ipynb。 （其实Notebook 就是个扩展名为 .ipynb 的大型 [JSON](https://link.zhihu.com/?target=http%3A//www.json.org/) 文件。）

<img class="size-full wp-image-14400" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-50.jpg" width="387" height="218" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-50.jpg)

点击下面的保存按钮，可以保存你的notebook文件。但 notebook 也会定期自动保存。

<img class="size-full wp-image-14402" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-52.jpg" width="621" height="266" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-52.jpg)

<img class="size-full wp-image-14404" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-54.jpg" width="720" height="278" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-54.jpg)

**3）重新运行所有单元格里的代码** **4）关闭 notebook文件** 通过在服务器主页上选中 notebook 旁边的复选框，然后点击“Shutdown”（关闭），你就可以关闭各个 notebook。 但是，在这样做之前，请确保你保存了工作！否则，在你上次保存后所做的任何更改都会丢失。同时如果不保存，你下次运行 notebook 时，你还需要重新运行代码。

<img class="size-full wp-image-14406" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-56.jpg" width="615" height="294" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-56.jpg)

**5）如何共享你的notebook？** 点击File->Download as，你可以选择多种格式下载你的notebook。一般我都会根据下面的用途来选择不同的下载格式： 1）如果我想和客户分享我的数据分析成果，我会选择将notebook下载为HTML文件。 2）如果我希望将自己的数据分析成果和代码嵌入到项目中，比如为药店管理系统做个数据分析子模块，我就会选择Python（.py）模块，这可以将我的代码融入项目中，成为子模块，方便和其他开发人员共同完成任务。 3）如果要在博客或文档中使用 notebook，我就选择Markdown格式。

<img class="size-full wp-image-14408" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-58.jpg" width="616" height="479" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-58.jpg)

**6）关闭Jupler notebook服务器** 通过在终端中按两次 Ctrl + C，可以关闭整个服务器。再次提醒，这会立即关闭所有运行中的 notebook，因此，请确保你保存了工作！ 关闭notebook服务器后，下次启动再打开notebook，当你继续在该notebook中写代码时，发现之前的变量无法访问了。需要你在该notebook的Kernerl选项卡中选择“Run All”重新编译下之前的代码。

<img class="size-full wp-image-14410" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-60.jpg" width="478" height="267" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-60.jpg)

7）安装的包在notebook中不可使用的问题： 是因为安装包的时候，不在当前notebook所在的python环境下安装了包，所以在这个python环境下找不到包。解决办法如下：

<img class="size-full wp-image-14412" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-62.jpg" width="720" height="199" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-62.jpg)

<img class="size-full wp-image-14414" src="http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-64.jpg" width="651" height="248" />

![](http://blog.echo.cool/wp-content/uploads/2018/05/jupyter-notebook基础使用-64.jpg)

如果你实践了上面的每一步，恭喜你，已经入门学会了 notebook。上面的命令也不需要你记住，只有你后面经常使用notebook，自然就熟练了。想想，你每天说话，会记住每个单词吗？当然不会，用的多了自然在大脑中就形成了记忆，而所谓的新技能学习，无非也是熟能生巧。