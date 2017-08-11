# cbeta 开源阅读计划

因为cbeta是用C++写的，我这里没有正版windows，所以一直是把cbeta光盘中的xml拷贝下来，自己处理之后阅读。
最近cbeta的xml格式发生了变化。所以重写了我的程序。随便共享出来给有需要的人。

## 主要目的

是能在线阅读大藏经,所以主要精力放在排版阅读上面

## 技术方式

1. 使用xslt来处理xml, 然后使用在xml中直接嵌入xslt的方式, 就可以直接在浏览器中阅读了。
如果希望自己使用的人, 可以自己搭建一个nginx服务器。将静态文件指向xml和tei.xsl,tei.css文件所在目录即可

2. 使用python来处理其他事情, 以及动态生成xslt文件， 主要是生成目录

## 工作到一半的时候发现已经有了
http://cbetaonline.dila.edu.tw/zh/T1579_011
但是技术没有公开, 作为一个练习项目继续写吧

## TODO
1. 目前只能阅读， 目录还没有加上
2. 加入全文搜索，应该是使用纯python的方式来处理

