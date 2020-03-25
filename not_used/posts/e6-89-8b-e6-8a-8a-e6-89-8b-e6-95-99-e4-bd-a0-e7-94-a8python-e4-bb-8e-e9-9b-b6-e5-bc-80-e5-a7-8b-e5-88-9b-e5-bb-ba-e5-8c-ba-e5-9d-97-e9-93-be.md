---
title: 手把手教你用Python从零开始创建区块链
tags:
  - python
url: 237.html
id: 237
categories:
  - Python
date: 2018-04-14 17:47:54
---

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/916854ce-ba51-403f-83e3-a0c0fe833cc3/640.gif?resizeSmall&width=832)

**导读：**如果你还没有听说过 3 点钟区块链群，说明你还不是链圈的人；如果你还没有加入 3 点钟区块链群，说明你还不是链圈的大佬；如果你还没有被 3 点钟区块链群刷屏，说明你还体会不到什么是“币圈一天，人间一年”。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/84848249-5978-4c93-afc7-bcda11076643/640.jpg?resizeSmall&width=832)

“三点钟区块链”无疑成为了大家春节期间焦虑的根源，而“区块链”注定是 2018 年被持续讨论、关注的行业性热点话题。 3 月 1 日，朱啸虎对正翻涌不断的区块链热潮再次开炮，在朋友圈一张画满区块链应用的图上，朱啸虎质疑：所有这些应用加在一起，有多少日活用户？“2000 年的互联网泡沫至少还有 eyeball，今天的区块链除了炒币外还有什么”？ 在此之前，朱啸虎在朋友圈转发了讽刺区块链投资热的文章《来，喝了这碗区块链的毒鸡汤！》，并声明：“不要拉我进任何 3 点钟群，有些风口宁愿错过，有些钱宁愿不赚，大家晚节保重。”朱啸虎还表示，说 ICO 是庞氏骗局是在侮辱庞氏骗局。 作为程序员的你，再不懂这个技术，2018 可能会被淘汰！下面和小编一起从十个幽默段子入门区块链吧！ **01 笑喷！区块链十个段子集锦** 1、假如你是一位女性，你男朋友每次跟你说一句肉麻的话或者承诺给你买东西，你都立刻录下来并且发给你的和他的所有闺蜜、同学、同事，还有各种群和朋友圈，让他再也无法抵赖，这叫区块链。 2、麻将是中国传统的区块链项目：四个矿工一组，先碰撞出 13 个数字正确哈希值的矿工可以获得记账权并得到奖励。不可篡改。因为说服其他三个人需要消耗太多算力和体力。 3、玩夜店的小姐姐和玩虚拟币的小哥哥们有几处相似：

*   都是自认聪明的优秀群体
*   不给自己赚钱的都是傻 X 屌丝
*   都认识很多大佬
*   都明白很多道理
*   都是在等自己涨价或者自己的虚拟币涨价被别人接盘

4、区块链是正经技术，各种币正不正经就不知道了。 5、吴三桂在山海关冲冠一怒，本质是为了争夺睡陈圆圆的权力；大佬们在区块链路上的互怼，本质是为了争夺割韭菜的权力。 6、新学期刚开始，儿子问老爸：「父亲工作一栏怎么填？是写币民吗？」老爸犹豫了一下说：「就写多家上市公司股东。」 7、最近数字货币很火，很多山寨币都是几倍几十倍的增长。很多炒币的开始飘飘然，叫嚣什么「一币一嫩模」。有朋友就问我要不要跟？我观点很简单：淘金热，一窝蜂淘金，风险很大。所以，让他们叫「一币一嫩模」去吧，不要跟风盲目炒币，我们应该赚他们的钱——去当嫩模！当嫩模！嫩模！ 8、我昨天遇见一币友，问他：「近来币市暴降，睡觉质量怎么样？」 他说：「还行，像婴儿般睡觉！」 我说：「羡慕了。」 他说：「是睡一个小时，醒了，然后哭一个小时，接着，再睡一个小时，起来再哭一个小时。」 9、老同志语重心长地对 80、90 后说：「别玩那些比特币，那些虚拟的玩意，做点实事在北京买个房、娶个媳妇，多好！」90 后回答说：「你们都把几千块钱成本的房子搞到10万一平米了。我们不另寻出路，搞一串串数字 10 万一个卖给你们，我们拿什么买得起房子啊？」 10、首先感谢公司拿出价值 100 万的比特币作为给员工的奖励，其次我觉得自己很幸运能拿到这 95 万的奖励，然后我觉得我还是要好好规划一下这 86 万的用处，毕竟 70 万也不是一笔小钱，我打算拿出 20 万给父母，剩下的 36 万暂时还没想好怎么用，总之，感谢公司价值 30 万的比特币的奖励，谢谢，祝大家和我一样都能得到这 15 万的奖励。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/93a79576-3378-4cd4-a873-14ae536874e7/640.jpg?resizeSmall&width=832)

**02 图解：大白话了解到底区块链是个啥？** **1\. what is 区块链**

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/c1216f5c-debd-4825-82ad-be65f83f62b8/640.jpg?resizeSmall&width=832)

“区块链仅仅是一门技术而已”，“比特币”仅仅是区块链技术的一种应用而已， 就好比，一个人会厨艺的技术，但是应用起他的厨艺可以做出“宫保鸡丁”、”鱼香肉丝”等各式的菜肴。 那么，到底“区块链”是个啥？我们这里借助网上一个比较流行的段子，将它用图形的形式展示给大家。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/3c26906e-422c-45fa-b07f-997ea07f55ad/640.jpg?resizeSmall&width=832)

我们可以将“比特币”抽象成“某荣的照片”如上图所示，如果网上很多用户想要得到某荣的照片，需要到一个固定的网站去搜索。 当然你也没其他地方可去嘛，那么好了，这个某榴网站天天给你弹出广告啊，小窗口啊，你都得忍着，没办法，因为就这一个地方可以获取嘛。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/5484b257-1db7-445f-9424-d5a7c43c138f/640.jpg?resizeSmall&width=832)

再者，这个网站突然被警察叔叔封杀了咋办？或者断电？断网？管他啥的，反正就是服务器崩溃了，那么悲剧的“某荣”粉丝们心爱的 2100 张照片将全部失去提供资源的场所。 这就是网上流传的新词“中心化”喽，他的弊端就是资源集中一起，抗风险容错性很弱。资源容易丢失。 那么，怎么解决这个问题呢？我们试想，能不能让每个“某荣”粉丝，都拥有这 2100 张照片呢？比如下图：

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/f3a9e424-d37f-4da6-a152-6cd6a73a0314/640.jpg?resizeSmall&width=832)

这样的话，貌似就不用在依赖那个“某榴”网站了呢。即使某个粉丝突然电脑崩溃，他随便找一个其他粉丝来获得这 2100 张照片，不愁了，不愁了。 后来，一个叫“某本聪”的一个虚拟人物提供了,一个拥有协议的某荣照片共享文件夹，用户可以从中获取照片，但是必须遵循协议。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/4dfb1025-dfc1-4227-9efe-4cc63ebf4e29/640.jpg?resizeSmall&width=832)

这样，每个粉丝都可以从这个文件夹中获取那 2100 张某荣的照片，但是全部获取的粉丝必须要遵循一个协议，当然是人家某本聪定义的协议啦。 “不得复制，修改，共享文件中的任意照片，粉丝们在共享文件夹中的任何行为都会被记录，并且是按照时间去记录！” 粉丝们这么喜爱某荣，而且不需要去某榴获取，当然就纷纷踊跃加入了~ 忽然，有一天，调皮的小 One 想要违背规则，在 2018 年 1 月 15 日中午 12 点删除编号为 1-100 的某荣照片。 根据协议，这个行为会被记录，并且会广播给其他粉丝。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/72da5e3a-20fa-4f69-8f0d-35bdb18413b3/640.jpg?resizeSmall&width=832)

照片到底被删除了么？当然不是，因为小露手里也有照片嘛，她收到广播后可以立刻恢复共享文件夹中已经删除的照片，小 One 永远别想对“共享文件夹”搞修改破坏，且所有行为都同步记录在其他用户的电脑里。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/5b8eb413-6660-42e1-8a47-b48b3762ef66/640.jpg?resizeSmall&width=832)

这就是区块链，数据分散存储，去中心化。按时间戳广播记录所有行为，无法修改、破坏数据源或造假。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/2e631778-7f97-4bda-8c4c-378ff9df0f4b/640.jpg?resizeSmall&width=832)

除非同一时刻炸掉 100 万个用户的电脑，或互联网消失，或世界毁灭....否则数据将永远存在~~

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/b34ac087-33d1-428d-8873-919cdbe49622/640.jpg?resizeSmall&width=832)

如何增加区块链保护的资源？“某本聪”又来了。他说，你们是可以在文件中添加某荣照片的，但是呢，你们各位必须达到某种“共识”？啥是“共识”，就是我们都承认的规则喽。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/6802d306-466e-4604-811b-946039b1d212/640.jpg?resizeSmall&width=832)

那到底是个啥共识呢？啊，小 One 和小露立刻了解了某本聪的意思，在每年规定的时间内，尽快拍出 100 张某荣的照片，这样就可以添加到“某荣共享文件夹”了，我们的资源就扩充了。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/4a17db2a-145f-4509-85c7-05e8e98f5efd/640.jpg?resizeSmall&width=832)

但是，好景不长。某本聪发现大量的拍照，冲击前 100，那很快就能达成了，拍照就没有难度了。 而且照片质量还差，好像谁都能轻易的添加照片资源，这样就保证不了某荣的照片质量了。于是，某本聪再次降临，增加拍照的共识难度。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/a2bf09f9-6353-46d8-adaa-a8acf9b4f4e8/640.jpg?resizeSmall&width=832)

小 One 和小露作为忠实的粉丝，怎能放弃，他们买了高端相机，让某荣摆出各种姿势，花费大量的时间和汗水完成了高质量的照片，当然自己也非常的辛苦。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/f525d132-61a8-46a7-b725-a58eb191c78e/640.jpg?resizeSmall&width=832)

这样高质量的照片就可以添加到“某荣的文件夹”中了。

**2\. 何为 ICO？**

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/f0d867ea-8eab-409b-803c-99a314381f2b/640.jpg?resizeSmall&width=832)

小 One 想：每张照片都是不可造假破坏的，所以具有唯一性，还有单独编号，给每一张照片估价，它不就值钱了吗？就像现实世界中无法复制的名画一样！ 小 One 就把之前的某荣照片，构造出来相应的“某荣币”，当然这个行为就向我们的政府通过国库的黄金数额发行等价的人民币类似啦。 估值呢，当然小 One 说的算啦，人家是照片的拥有者嘛。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/8e74dc31-2ef0-4c3d-9f5f-9b3f5353a5ea/640.jpg?resizeSmall&width=832)

为了证实某荣币 5W 块一个，小 One 首先购买了 2100 个中的 1100 个，剩下的发行给吃瓜群众们啦，我们已经用 5W 买一个，说明他已经值这个价钱啦，剩下 1000 个大家一起买吧。 这样的话如果 2100 个全部认购出去，2100 个某荣币可以就估值 1.05 亿块哦~这种通过数字货币的发行而得到融资的过程就是 ICO 啦。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/1ec293ab-66a1-496a-82b3-37bcdef638ff/640.jpg?resizeSmall&width=832)

根据这个图的含义，如果小 One 和小露是一个可信任的机构或者公众人物，还是可以相信他们的，当然啦也会有很多不法分子恶意发行货币来套现的。 这也是我们国家为什么禁止 ICO 发行的原因啦，因为目前没有一个完善的 ICO 监管条例能够保证发行货币的机构的可信任性和合法的监管他们，所以吃瓜群众们要自己承担风险找到一个可信的机构。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/7414aa36-33e3-495e-9d41-c679c41ec5ec/640.jpg?resizeSmall&width=832)

这样 2100 个某荣币全部认购成功，基金成立，这就是 ICO。当然吃瓜群众也可以继续拍照创造某荣币，就是有点难罢了。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/7f9fac53-5194-46fb-9193-40a73a36548f/640.jpg?resizeSmall&width=832)

现在各位了解什么是区块链和 ICO 了吧~下面手把手教你如何用 Python 语言创建一个区块链？ **03 用 Python 从 0 开始创建一个区块链** 对数字货币的崛起感到新奇的我们，并且想知道其背后的技术——区块链是怎样实现的。本文通过 Python 构建一个区块链可以加深对区块链的理解。 **1\. 准备工作** 本文要求读者对 Python 有基本的理解，能读写基本的 Python，并且需要对 HTTP 请求有基本的了解。 我们知道区块链是由区块的记录构成的不可变、有序的链结构，记录可以是交易、文件或任何你想要的数据，重要的是它们是通过哈希值（hashes）链接起来的。 如果你还不是很了解哈希，可以查看这篇文章https://learncryptography.com/hash-functions/what-are-hash-functions。 **（1）环境准备：** 环境准备，确保已经安装 Python3.6+、pip、Flask、requests。 **（2）安装方法：**

pip install Flask==0.12.2 requests==2.18.4

同时还需要一个 HTTP 客户端，比如 Postman、cURL 或其他客户端。 参考源代码（原代码在我翻译的时候，无法运行，我 fork 了一份，修复了其中的错误，并添加了翻译，感谢 star）。 **2\. 开始创建 Blockchain** 新建一个文件 blockchain.py，本文所有的代码都写在这一个文件中，可以随时参考源代码。 **（1）Blockchain 类** 首先创建一个 Blockchain 类，在构造函数中创建了两个列表，一个用于储存区块链，一个用于储存交易。 以下是 Blockchain 类的框架：

classBlockchain(object): def\_\_init\_\_(self): self.chain = \[\] self.current\_transactions = \[\] defnew\_block(self): # Creates a new Block and adds it to the chain pass defnew\_transaction(self): # Adds a new transaction to the list of transactions pass @staticmethod defhash(block): # Hashes a Block pass @property deflast\_block(self): # Returns the last Block in the chain pass

Blockchain 类用来管理链条，它能存储交易、加入新块等，下面我们来进一步完善这些方法。 **（2）块结构** 每个区块包含属性：索引（index）、Unix 时间戳（timestamp）、交易列表（transactions）、工作量证明（稍后解释）以及前一个区块的 Hash 值。 以下是一个区块的结构：

block = { 'index': 1, 'timestamp': 1506057125.900785, 'transactions': \[ { 'sender': "8527147fe1f5426f9dd545de4b27ee00", 'recipient': "a77f5cdfa2934df3954a5c7c7da5df1f", 'amount': 5, } \], 'proof': 324984774000, 'previous_hash': "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824" }

到这里区块链的概念就清楚了，每个新的区块都包含上一个区块的 Hash，这是关键的一点，它保障了区块链的不可变性。 如果攻击者破坏了前面的某个区块，那么后面所有区块的Hash都会变得不正确。不理解的话，慢慢消化，可参考{% post_link whatbc 区块链技术原理 %}。 **（3）加入交易** 接下来我们需要添加一个交易，来完善下 new_transaction 方法：

classBlockchain(object): ... defnew\_transaction(self, sender, recipient, amount): """ 生成新交易信息，信息将加入到下一个待挖的区块中 :param sender: <str> Address of the Sender :param recipient: <str> Address of the Recipient :param amount: <int> Amount :return: <int> The index of the Block that will hold this transaction """ self.current\_transactions.append({ 'sender': sender, 'recipient': recipient, 'amount': amount, }) return self.last_block\['index'\] + 1

方法向列表中添加一个交易记录，并返回该记录将被添加到的区块(下一个待挖掘的区块)的索引，等下在用户提交交易时会有用。 **（4）创建新块** 当 Blockchain 实例化后，我们需要构造一个创世块（没有前区块的第一个区块），并且给它加上一个工作量证明。每个区块都需要经过工作量证明，俗称挖矿，稍后会继续讲解。 为了构造创世块，我们还需要完善 new\_block()，new\_transaction() 和hash() 方法：

import hashlib import json from time import time classBlockchain(object): def\_\_init\_\_(self): self.current\_transactions = \[\] self.chain = \[\] # Create the genesis block self.new\_block(previous\_hash=1, proof=100) defnew\_block(self, proof, previous\_hash=None): """ 生成新块 :param proof: <int> The proof given by the Proof of Work algorithm :param previous\_hash: (Optional) <str> Hash of previous Block :return: <dict> New Block """ block = { 'index': len(self.chain) + 1, 'timestamp': time(), 'transactions': self.current\_transactions, 'proof': proof, 'previous\_hash': previous\_hash or self.hash(self.chain\[-1\]), } # Reset the current list of transactions self.current\_transactions = \[\] self.chain.append(block) return block defnew\_transaction(self, sender, recipient, amount): """ 生成新交易信息，信息将加入到下一个待挖的区块中 :param sender: <str> Address of the Sender :param recipient: <str> Address of the Recipient :param amount: <int> Amount :return: <int> The index of the Block that will hold this transaction """ self.current\_transactions.append({ 'sender': sender, 'recipient': recipient, 'amount': amount, }) return self.last\_block\['index'\] + 1 @property deflast\_block(self): return self.chain\[-1\] @staticmethod defhash(block): """ 生成块的 SHA-256 hash值 :param block: <dict> Block :return: <str> """ # We must make sure that the Dictionary is Ordered, or we'll have inconsistent hashes block\_string = json.dumps(block, sort\_keys=True).encode() return hashlib.sha256(block_string).hexdigest()

通过上面的代码和注释可以对区块链有直观的了解，接下来我们看看区块是怎么挖出来的。 **（5）理解工作量证明** 新的区块依赖工作量证明算法（PoW）来构造。PoW 的目标是找出一个符合特定条件的数字，这个数字很难计算出来，但容易验证。这就是工作量证明的核心思想。 为了方便理解，举个例子： 假设一个整数 x 乘以另一个整数 y 的积的 Hash 值必须以 0 结尾，即 hash(x * y) = ac23dc...0。设变量 x = 5，求 y 的值？ 用 Python 实现如下：

from hashlib import sha256 x = 5 y = 0  # y未知 while sha256(f'{x*y}'.encode()).hexdigest()\[-1\] != "0": y += 1 print(f'The solution is y = {y}')

结果是：y = 21，因为：

hash(5 * 21) = 1253e9373e...5e3600155e860

在比特币中，使用称为 Hashcash 的工作量证明算法，它和上面的问题很类似，矿工们为了争夺创建区块的权利而争相计算结果。 通常，计算难度与目标字符串需要满足的特定字符的数量成正比，矿工算出结果后，会获得比特币奖励。当然，在网络上非常容易验证这个结果。 **（6）实现工作量证明** 让我们来实现一个相似 PoW 算法，规则是：寻找一个数 p，使得它与前一个区块的 proof 拼接成的字符串的 Hash 值以 4 个零开头。

import hashlib import json from time import time from uuid import uuid4 classBlockchain(object): ... defproof\_of\_work(self, last\_proof): """ 简单的工作量证明: - 查找一个 p' 使得 hash(pp') 以4个0开头 - p 是上一个块的证明,  p' 是当前的证明 :param last\_proof: <int> :return: <int> """ proof = 0 while self.valid\_proof(last\_proof, proof) isFalse: proof += 1 return proof @staticmethod defvalid\_proof(last\_proof, proof): """ 验证证明: 是否hash(last\_proof, proof)以4个0开头? :param last\_proof: <int> Previous Proof :param proof: <int> Current Proof :return: <bool> True if correct, False if not. """ guess = f'{last\_proof}{proof}'.encode() guess\_hash = hashlib.sha256(guess).hexdigest() return guess_hash\[:4\] == "0000"

衡量算法复杂度的办法是修改零开头的个数。使用 4 个零来用于演示，你会发现多一个零都会大大增加计算出结果所需的时间。 现在 Blockchain 类基本已经完成了，接下来使用 HTTP requests 来进行交互。 **2\. Blockchain 作为 API 接口** 我们将使用 Python Flask 框架，这是一个轻量 Web 应用框架，它方便将网络请求映射到 Python 函数，现在我们来让 Blockchain 运行在 Flask Web 上。 我们将创建三个接口：

*   **/transactions/new 创建一个交易并添加到区块**
*   **/mine 告诉服务器去挖掘新的区块**
*   **/chain 返回整个区块链**

**（1）创建节点** 我们的“Flask 服务器”将扮演区块链网络中的一个节点，我们先添加一些框架代码：

import hashlib import json from textwrap import dedent from time import time from uuid import uuid4 from flask import Flask classBlockchain(object): ... # Instantiate our Node app = Flask(\_\_name\_\_) # Generate a globally unique address for this node node\_identifier = str(uuid4()).replace('-', '') # Instantiate the Blockchain blockchain = Blockchain() @app.route('/mine', methods=\['GET'\]) defmine(): return"We'll mine a new Block" @app.route('/transactions/new', methods=\['POST'\]) defnew\_transaction(): return"We'll add a new transaction" @app.route('/chain', methods=\['GET'\]) deffull\_chain(): response = { 'chain': blockchain.chain, 'length': len(blockchain.chain), } return jsonify(response), 200 if \_\_name__ == '\_\_main\_\_': app.run(host='0.0.0.0', port=5000)

简单的说明一下以上代码：

*   **第 15 行：**创建一个节点。
*   **第 18 行：**为节点创建一个随机的名字。
*   **第 21 行：**实例 Blockchain 类。
*   **第 24–26 行：**创建 /mine GET 接口。
*   **第 28–30 行：**创建 /transactions/new POST 接口,可以给接口发送交易数据。
*   **第 32–38 行：**创建 /chain 接口, 返回整个区块链。
*   **第 40–41 行：**服务运行在端口 5000 上。

**（2）发送交易** 发送到节点的交易数据结构如下：

{ "sender": "my address", "recipient": "someone else's address", "amount": 5 }

之前已经有添加交易的方法，基于接口来添加交易就很简单了：

import hashlib import json from textwrap import dedent from time import time from uuid import uuid4 from flask import Flask, jsonify, request ... @app.route('/transactions/new', methods=\['POST'\]) defnew\_transaction(): values = request.get\_json() # Check that the required fields are in the POST'ed data required = \['sender', 'recipient', 'amount'\] ifnot all(k in values for k in required): return'Missing values', 400 # Create a new Transaction index = blockchain.new_transaction(values\['sender'\], values\['recipient'\], values\['amount'\]) response = {'message': f'Transaction will be added to Block {index}'} return jsonify(response), 201

**（3）挖矿** 挖矿正是神奇所在，它很简单，做了以下三件事：

*   **计算工作量证明 PoW。**
*   **通过新增一个交易授予矿工（自己）一个币。**
*   **构造新区块并将其添加到链中。**

import hashlib import json from textwrap import dedent from time import time from uuid import uuid4 from flask import Flask, jsonify, request ... import hashlib import json from time import time from uuid import uuid4 from flask import Flask, jsonify, request ... @app.route('/mine', methods=\['GET'\]) defmine(): # We run the proof of work algorithm to get the next proof... last\_block = blockchain.last\_block last\_proof = last\_block\['proof'\] proof = blockchain.proof\_of\_work(last\_proof) # 给工作量证明的节点提供奖励. # 发送者为 "0" 表明是新挖出的币 blockchain.new\_transaction( sender="0", recipient=node\_identifier, amount=1, ) # Forge the new Block by adding it to the chain block = blockchain.new\_block(proof) response = { 'message': "New Block Forged", 'index': block\['index'\], 'transactions': block\['transactions'\], 'proof': block\['proof'\], 'previous\_hash': block\['previous\_hash'\], } return jsonify(response), 200

注意交易的接收者是我们自己的服务器节点，我们做的大部分工作都只是围绕 Blockchain 类方法进行交互。到此，我们的区块链就算完成了，我们来实际运行下。 **（4）运行区块链** 你可以使用 cURL 或 Postman 去和 API 进行交互。 启动 server：

$ python blockchain.py * Runing on http://127.0.0.1:5000/ (Press CTRL+C to quit)

让我们通过请求 http://localhost:5000/mine 来进行挖矿：

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/d280e89e-5de1-44b5-ba01-4dc816705c51/640.jpg?resizeSmall&width=832)

通过 post 请求，添加一个新交易：

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/c3939c48-af1a-46ae-b214-c0ea37620140/640.jpg?resizeSmall&width=832)

如果不是使用 Postman，则用以下的 cURL 语句也是一样的：

$ curl -X POST -H "Content-Type: application/json" -d '{ "sender": "d4ee26eee15148ee92c6cd394edd974e", "recipient": "someone-other-address", "amount": 5 }' "http://localhost:5000/transactions/new"

在挖了两次矿之后，就有 3 个块了，通过请求 http://localhost:5000/chain 可以得到所有的块信息。

{ "chain": \[ { "index": 1, "previous\_hash": 1, "proof": 100, "timestamp": 1506280650.770839, "transactions": \[\] }, { "index": 2, "previous\_hash": "c099bc...bfb7", "proof": 35293, "timestamp": 1506280664.717925, "transactions": \[ { "amount": 1, "recipient": "8bbcb347e0634905b0cac7955bae152b", "sender": "0" } \] }, { "index": 3, "previous_hash": "eff91a...10f2", "proof": 35089, "timestamp": 1506280666.1086972, "transactions": \[ { "amount": 1, "recipient": "8bbcb347e0634905b0cac7955bae152b", "sender": "0" } \] } \], "length": 3 }

**3\. 一致性（共识）** 我们已经有了一个基本的区块链可以接受交易和挖矿，但是区块链系统应该是分布式的。 既然是分布式的，那么我们究竟拿什么保证所有节点有同样的链呢？这就是一致性问题，我们要想在网络上有多个节点，就必须实现一个一致性的算法。 **（1）注册节点** 在实现一致性算法之前，我们需要找到一种方式让一个节点知道它相邻的节点。 每个节点都需要保存一份包含网络中其他节点的记录，因此让我们新增几个接口：

*   /nodes/register 接收 URL 形式的新节点列表。
*   /nodes/resolve 执行一致性算法，解决任何冲突，确保节点拥有正确的链。

我们修改下 Blockchain 的 init 函数并提供一个注册节点方法：

... from urllib.parse import urlparse ... classBlockchain(object): def\_\_init\_\_(self): ... self.nodes = set() ... defregister\_node(self, address): """ Add a new node to the list of nodes :param address: <str> Address of node. Eg. 'http://192.168.0.5:5000' :return: None """ parsed\_url = urlparse(address) self.nodes.add(parsed_url.netloc)

我们用 set 来储存节点，这是一种避免重复添加节点的简单方法。 **（2）实现共识算法** 前面提到，冲突是指不同的节点拥有不同的链，为了解决这个问题，规定最长的、有效的链才是最终的链，换句话说，网络中有效最长链才是实际的链。 我们使用以下的算法，来达到网络中的共识：

... import requests classBlockchain(object) ... defvalid\_chain(self, chain): """ Determine if a given blockchain is valid :param chain: <list> A blockchain :return: <bool> True if valid, False if not """ last\_block = chain\[0\] current\_index = 1 while current\_index < len(chain): block = chain\[current\_index\] print(f'{last\_block}') print(f'{block}') print("\\n-----------\\n") # Check that the hash of the block is correct if block\['previous\_hash'\] != self.hash(last\_block): return False # Check that the Proof of Work is correct ifnotself.valid\_proof(last\_block\['proof'\], block\['proof'\]): return False last\_block = block current\_index += 1 return True defresolve\_conflicts(self): """ 共识算法解决冲突 使用网络中最长的链. :return: <bool> True 如果链被取代, 否则为False """ neighbours = self.nodes new\_chain = None # We're only looking for chains longer than ours max\_length = len(self.chain) # Grab and verify the chains from all the nodes in our network for node inneighbours: response = requests.get(f'http://{node}/chain') if response.status\_code == 200: length = response.json()\['length'\] chain = response.json()\['chain'\] # Check if the length is longer and the chain is valid if length > max\_length andself.valid\_chain(chain): max\_length = length new\_chain = chain # Replace our chain if we discovered a new, valid chain longer than ours ifnew\_chain: self.chain = new\_chain return True return False

第一个方法 valid\_chain() 用来检查是否是有效链，遍历每个块验证 hash 和 proof。 第二个方法 resolve\_conflicts() 用来解决冲突，遍历所有的邻居节点，并用上一个方法检查链的有效性， 如果发现有效更长链，就替换掉自己的链。 让我们添加两个路由，一个用来注册节点，一个用来解决冲突。

@app.route('/nodes/register', methods=\['POST'\]) defregister\_nodes(): values = request.get\_json() nodes = values.get('nodes') if nodes is None: return"Error: Please supply a valid list of nodes", 400 for node innodes: blockchain.register\_node(node) response = { 'message': 'New nodes have been added', 'total\_nodes': list(blockchain.nodes), } return jsonify(response), 201 @app.route('/nodes/resolve', methods=\['GET'\]) defconsensus(): replaced = blockchain.resolve\_conflicts() ifreplaced: response = { 'message': 'Our chain was replaced', 'new\_chain': blockchain.chain } else: response = { 'message': 'Our chain is authoritative', 'chain': blockchain.chain } return jsonify(response), 200

你可以在不同的机器运行节点，或在一台机机开启不同的网络端口来模拟多节点的网络。 这里在同一台机器开启不同的端口演示，在不同的终端运行以下命令，就启动了两个节点：

*   **http://localhost:5000 **
*   **http://localhost:5001**

pipenvrunpythonblockchain.py pipenvrunpythonblockchain.py-p 5001

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/392fe18b-8eaa-4466-a0f1-188d48df567b/640.jpg?resizeSmall&width=832)

然后在节点 2 上挖两个块，确保是更长的链，然后在节点 1 上访问接口 /nodes/resolve，这时节点 1 的链会通过共识算法被节点 2 的链取代。

![](https://app.yinxiang.com/shard/s71/nl/17011625/21ea6c50-8068-4c6b-97e5-9a61079ae0a1/res/3f99434b-1fa4-47a0-b567-3e4956c54c28/640.jpg?resizeSmall&width=832)

好啦，你可以邀请朋友们一起来测试你的区块链。