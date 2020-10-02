---
layout: post
title:  浪潮面试笔试
date:   2015-10-09 10:22:34
categories: seek-work
---
链接：[http://baodian.yjbys.com/inspur/6-2.html](http://baodian.yjbys.com/inspur/6-2.html)
# 1.上机试题 #
1.用c 语言输入一个字符串,再输出,并且去掉两边的空格。
[http://zhanchangwen.github.io/blog/seek-work/2015/10/10/c-trim.html](http://zhanchangwen.github.io/blog/seek-work/2015/10/10/c-trim.html)

2.简述b+树和b-树的算法思想。

B-树，又名B树、B-树、B_树。B即Balanced，平衡的意思。

B-树是一种多路搜索树（并不一定是二叉的）

一棵m阶B树(balanced tree of order m)是一棵平衡的m路搜索树。它或者是空树，或者是满足下列性质的树：

1. 根结点至少有两个子女；
1. 每个非根节点所包含的关键字个数 j 满足：┌m/2┐ - 1 <= j <= m - 1；
1. 除根结点以外的所有结点（不包括叶子结点）的度数正好是关键字总数加1，故内部子树个数 k 满足：┌m/2┐ <= k <= m ；
1. 所有的叶子结点都位于同一层。

B+ 树是一种树数据结构，是一个n叉树，每个节点通常有多个孩子，一颗B+树包含根节点、内部节点和叶子节点。根节点可能是一个叶子节点，也可能是一个包含两个或两个以上孩子节点的节点。<br>
B+ 树的特点是能够保持数据稳定有序，其插入与修改拥有较稳定的对数时间复杂度。B+ 树元素自底向上插入。


3.简述先序遍历,中序遍历,后序遍历的算法思想。

先序遍历：[百度百科-先序遍历](http://baike.baidu.com/link?url=-zY-vQfup8lfV5rQ9FVNTNsOVDpOYD0Q3hQ3p0LvBolayUwnwxH0xqKtN3V671fWnilsyh_OyBe8OR_g7KTgSa)

首先访问根结点然后遍历左子树，最后遍历右子树。在遍历左、右子树时，仍然先访问根结点，然后遍历左子树，最后遍历右子树，如果二叉树为空则返回。

中序遍历：[百度百科-中序遍历](http://baike.baidu.com/link?url=zvY99E5DTuibEfqMRdCLZxZLQyQe0GevVw6PBcngDnrYfyXNod3ny5xXdDsWNIPANL5Q9IsSya-0RxvnLDQUAq)

首先遍历左子树，然后访问根结点，最后遍历右子树。在遍历左、右子树时，仍然先遍历左子树，再访问根结点，最后遍历右子树。

后序遍历：[百度百科-后序遍历](http://baike.baidu.com/link?url=SfHHT2NDlLxcpJGAMtYyhS623aJpilcI_l8q3u9WA_ACSs63HH92liPaGcccEEFdy0vAg5G4X4Ypl1nP67Syva)

首先遍历左子树，然后遍历右子树，最后访问根结点，在遍历左、右子树时，仍然先遍历左子树，然后遍历右子树，最后遍历根结点。

算法核心思想：

首先要搞清楚先序、中序、后序的非递归算法共同之处：用栈来保存先前走过的路径，以便可以在访问完子树后,可以利用栈中的信息,回退到当前节点的双亲节点,进行下一步操作。
后序遍历的非递归算法是三种顺序中最复杂的，原因在于，后序遍历是先访问左、右子树,再访问根节点，而在非递归算法中，利用栈回退到时，并不知道是从左子树回退到根节点，还是从右子树回退到根节点，如果从左子树回退到根节点，此时就应该去访问右子树，而如果从右子树回退到根节点，此时就应该访问根节点。所以相比前序和后序，必须得在压栈时添加信息，以便在退栈时可以知道是从左子树返回，还是从右子树返回进而决定下一步的操作。

4.1000个苹果，分别将它们装进10个篮子里。 

要求：当要取1~1000个数之中任意数个苹果时，必须整整地取苹果（即不能在一篮苹果中分零，只取其中的几个）

请将每个篮子中的苹果个数写出来。

