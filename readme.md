# cbeta 大藏经(大正藏)开源阅读计划  (做最好的开源阅藏程序)

因为cbeta是用C++写的，我这里没有正版windows，所以一直是把cbeta光盘中的xml拷贝下来，自己处理之后阅读。
最近cbeta的xml格式发生了变化。所以重写了我的程序。随便共享出来给有需要的人。

## 主要特点

1. 读经！读经！读经！只有这一个目的。目前网络上的藏经网站实在是多，但是都只是收藏佛经，而阅读则非常的费劲。
2. 同时支持简体繁体搜索和阅读
3. 可以在阅读的时候划词/划字的方式查询词典/字典
4. 语音合成，自动阅读经文
5. 修正了一些cbeta的显示错误
6. 除叠辅音外的悉曇字使用unicode显示

## 哲学或者主旨、版权
1. 佛法是人类文明最珍贵的精华，对东方文化，及人类文明，有深远的影响。是法住法位，非佛作亦非余人作。所以为了传播佛法，禁止商业行为，是十分愚蠢的。
2. 这些代码只是我自己用的，为了自己用的舒服，开放出来也只是基于共享精神，所以如果有需要的功能，可以给我发邮件，如果我感兴趣而且有时间也许会加上
3. 版权问题：这些代码都是完全公开的，没有版权，以后考虑加入MIT或者公共域等其他类似的版权，你可以拿去完全的修改，公开发行，去掉我的名字，融资上市挣钱，这些我都不关心
4. 禁止行为：任何导致作者有可能不能使用自己的代码的行为都是禁止的。我在任何情况下都完全拥有使用自己代码的权力，所有权、著作权，修改权，无论你怎么修改这些代码。
5. 免责声明：因为没有版权，所以如果(因为使用此软件)出了什么事情，都是你自己的事儿，把你的电脑搞砸了，和老婆吵架了，或者破坏了世界和平，毁灭了宇宙，都跟我一点关系都没有，不要来找我！本人不保障此软件的安全性，不保障软件中没有包含病毒、蠕虫或者其他任何有害程序。你应该自己保障这些事情
6. 法律保障：你把这些拿去使用不会有任何法律上的烦恼，因为采用的一切技术都是free的技术，不需要你购买开发工具，不需要你购买操作系统，不需要你购买数据库，不需要你购买类似java或者VC++这样由商业公司完全控制的软件
7. 戒律保障：因为全部使用自由软件，所以你可以持最严格的戒律，尤其是盗戒，保持戒律清净，不用担心盗版软件，也不用担心商业公司在你使用一段时间之后修改了软件条款，而你处于闭关状态无法及时响应。这是我唯一敢保障的。
8. 因为这是自由软件，但是不是免费软件，所以此资源完全可以通过商业途径传播，可以倒找钱、免费、高价、天价或者宇宙价出售光盘/U盘/硬盘, 可以随有价光盘/U盘一起赠送！这些不需要本人的任何授权！也不需要通知本人。

## cbeta存在的问题
1. 使用图片显示悉昙字,蘭扎字，使用 组字式显示异体字,显示效果差
2. 光盘版是C++写的，Windows only
3. 光盘版不稳定，容易死机，速度也不理想
4. 原始xml文件的质量存在问题，需要做一个清洗
5. 在注释问题字段的时候使用两个anchor标签夹在一起的做法。导致获得这些字段非常困难
6. 使用<byline cb:type="Author">表示作者, <byline cb:type="translator">表示译者，混用大小写和中英文，还同时使用cb:jl_byline，含义模糊
7. <p rend="inline">的写法，本来就是一个行内元素,导致T55n2157_024.xml显示不正常
8. cbeta的note标注有时候显示的是勘误后的文字，有时候显示的是勘误前的文字。让人迷惑
9. 破折号的使用太频繁了，用了好多字体，都无法正确显示，太容易和一弄混了。还是应该删掉，简单的使用逗号表示即可
10. cbeta这个网站实在太慢了。我曾经在我的诺基亚N9手机上建立了一个网站，比cbeta快多了

## 技术方式和预期效果

1. 速度.目前来看相比CBETA速度快上很多。完全不消耗服务器资源。对浏览器的消耗也非常小。速度非常快。CBETA在多处有卡顿的现象。原因不明，阅读体验不佳
目前唯一发现有些微卡顿的是' 胎藏梵字真言上卷', (T18/T18n0854_001.xml),用时0.5秒降为0.09秒，原因是使用了太多的图片和文件比较大所导致;优化速度后最大(2.7M)的文件'朝鮮佛教通史'(B31n0170_003.xml)由0.9秒降低为0.45秒，
原来速度最慢的K35n1257_025由2.5秒降为0.25秒,已经可用
2. 代码非常少。修改部署容易
3. 正确的显示经文
4. 简体字与繁体字都可以正常搜索内容
5. 自制的悉昙字字体已经正常, 使用Unicode10.0的码表来显现, ttf文件只有9k大小
6. 整体程序非常简单。只有一个tei.xsl文件和一个tei.css文件作为显示效果。而阅读效果比较好。修改简单方便，适合长期阅读藏经使用。


## 技术方式

1. 使用xslt来处理xml, 然后使用在xml中直接嵌入xslt的方式, 就可以直接在浏览器中阅读了。
如果希望自己使用的人, 可以自己搭建一个nginx服务器。将静态文件指向xml和tei.xsl,tei.css文件所在目录即可

2. 使用python来处理其他事情, 以及动态生成xslt文件， 主要是生成目录

3. 尽量少的使用js控制， 对搜索引擎友好

4. 在线直接阅读xml文件. 不单独生成html，占用空间小。其他格式文件也可以直接在线生成

## 使用说明

1. 首先把cbeta中的xml文件拷贝出来到一个目录比如TMP，然后拷贝static/tei.xsl和static/tei.css两个文件到TMP目录下的stylesheet目录。
2. 启动nginx服务器，设置静态目录为TMP。一个不错的阅经环境就设置完成了

## 文件列表
1. static/tei.xsl 主体程序
2. static/tei.css css效果文件
3. static/siddham.ttf 符合unicode10.0的悉昙体字库
4. static/siddham.sfd 符合unicode10.0的悉昙体字库的fontforg文件，可以根据这个文件继续修改字库
5. static/siddham.woff 符合unicode10.0的悉昙体字库,可以通过webfont方式使用悉昙体字库，以便读者不用安装字库即可阅读悉昙体
6. terms.txt  佛教词汇大全，目前搜集了不到8万词汇，用来给藏经分词用的, 以便全文检索使用
7. w_normal.txt 制作的组合字表,相比原光盘的更加清晰, 用来清洗xml文档
8. w_norm2.txt 制作的未知组合字表, 需要填写
9. yoga 目录,打算后期为瑜伽师地论做现代化标点
10. reader.py python的web程序入口, 提供目录、搜索等服务
11.  static/bulei_sutra_sch.lst
    static/cangjian.lst
    static/sutra_sch.lst
    目录文件
12. temp目录, 页面模板文件

## 字库

1. 网站整体上是使用冬青黑体显示主要文字，使用SimSun显示标点符号，你可以随意修改为自己喜欢的字体
2. 建议下载花園明朝(HanaMin)字体以便显示生僻字  http://fonts.jp/hanazono/ 或者 http://ctext.org/font-test-page/zh, 因为花园字体是自由字体，尤其是花園明朝B一定要安装

## 浏览器兼容性
1. 主流浏览器: firefox、opera、chrome、safari、搜狗浏览器、IOS手机等主流浏览器都没有发现任何问题
2. 360浏览器在调整兼容性之后可以正常使用了。但是有些地方渲染比较奇怪
3. 微软系浏览器: Edge 12、ie11也可以翻页了，一切正常
4. ie8已经可以使用了，只是导航条无法固定
5. 终端浏览器: links2、w3m、lynx都无法使用
6. 因为导航需要探测文件存在与否，所以可能出现文件不存在的警告是正常的
7. 应该只能使用xslt1.0版本
8. firefox对勘误注释无法渲染为红色(anchor标签的问题)

| 浏览器        | 渲染引擎      | xslt版本| 
| ------------- |:-------------:| -------:| 
| 360           | Microsoft     |  1      |
| chrome        | libxslt       |  1.0    |
| Edge          | Microsoft     |  1      |
| firefox       | Transformiix  |  1.0    |
| opera         | libxslt       |  1.0    |
| safari        | libxslt       |  1.0    |
| 搜狗          | libxslt       |  1.0    |
| midori        | libxslt       |  1.0    |
| ie8           | Microsoft     |  1      |



## 工作到一半的时候发现已经有了
http://cbetaonline.dila.edu.tw/zh/T1579_011
但是技术没有公开, 而且还有显示问题

## TODO
1. 翻页不完善，需要的代码交互太多了; 而且浏览器需要多次访问服务器
2. 使用whoosh方案做全文搜索，支持复杂的查询语法, 使查询变得更加简单
3. 做一个组字式的替换表，以便在阅读中显示正常汉字
4. 删除悉昙字的图片，使用Unicode10.0的字来显现。目前字体做了一半，不会做那种可以移动的符号
5. 删除蘭扎字的图片，暂时设想使用悉昙字的变体来实现
6. 删除异体字和组字式
7. 删除g标签中的错误
8. 对悉昙体叠辅音的支持，暂时没空做了
9. 对登录用户保存书签
10. 登录用户自定义xsl, css
11. 悉昙体同时使用拉丁和悉昙字母搜索

## DEMO

1. 可以在 [这里](http://45.76.171.153:8000/mulu) 看到演示效果

# 查询使用的语法
1. 关键字是AND、OR、NOT。搜索域是title、author, 可以随意组合,使用()
2. 例如搜索阿含经中的一段话,使用如下语句:  比丘集讲堂 AND title:阿含经

## 目前存在的问题
1. 搜索生成的索引文件太大了, 接近2.5G，查找一次使用时间太长，需要3~10秒。搜索结果不理想
2. 悉昙体不能处理叠辅音。叠辅音的显示效果很差, 单辅音的显示效果就比较好
3. 翻页需要去检测文件是否存在。如果文件不存在IE会停止处理xml文件，其他浏览器则简单的在控制台打印一条警告
4. 应该只能使用xslt1.0版本, 无法做到跨文件目录跳转(没有base-uri() and document-uri()),解决方法: 在自生成的xml中，在cb:mulu中添加一个属性，内容为当前文件名
5. 在注释附近的字在查询字典的时候，会和注释链接到一起，导致显示不正常
6. 跨文件目录无法合并目录树，每个文件都单独显示目录树
7. 语音合成需要CUDA做深度神经网络计算，目前没钱买，用纯CPU的方案先对付用吧

## 联系方式
可以通过wenping_zhao@126.com与我联系使用中的问题

