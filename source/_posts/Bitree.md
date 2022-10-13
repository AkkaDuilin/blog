---
title: 树相关知识集合
tags: 

    - C++
    - 树
copyright: true
date: 2021-12-13 23:57:30
permalink:
categories:

    - 数据结构
description:
image:
---

<a href="https://sm.ms/image/xrORW4XFJqaLNTo" target="_blank"><img src="https://s2.loli.net/2021/12/15/xrORW4XFJqaLNTo.png" ></a>

**前言**

整理一下二叉树的知识点

*不定期更新  ︿(￣︶￣)︿*


<!-- more -->

# 二叉树基础

## 定义
一棵二叉树是结点的一个有限集合，该集合或者为空，或者是由一个根结点加上两棵分别称为左子树和右子树的、互不相交的二叉树组成。二又树的特点是每个结点最多有两个子女，分别称为该结点的左子女和右子女。在二又树中不存在度大于2的结点，并且二又树的子树有左、右之分，其子树的次序不能颠倒。二又树是分支数最大不超过2的有根有序树。它可能有5种不同的形态。
## 性质
1. 在二叉树的第i层最多有2^(i-1)个结点
2. 深度为k的二叉树最有2^k - 1 个结点 
3. 叶子结点数等于度为2的结点数加1

# 完全二叉树

## 定义
一棵深度为k的有n个结点的二叉树，对树中的结点按从上至下、从左到右的顺序进行编号，如果编号为i（1≤i≤n）的结点与满二叉树中编号为i的结点在二叉树中的位置相同，则这棵二叉树称为完全二叉树。

## 性质
1.  具有n个结点的完全二叉树的深度log2(n+1)
2.  如果对一棵有n个结点的完全二叉树的结点按层序编号, 则对任一结点i (1≤i≤n) 有: 
    如果i=1, 则结点i是二叉树的根, 无双亲;
    如果i>1, 则其双亲parent (i) 是结点[i/2]. 
    如果2i>n, 则结点i无左孩子, 否则其左孩子lchild (i) 是结点2i; 
    如果2i+1>n, 则结点i无右孩子, 否则其右孩子rchild (i) 是结点2i+1.

3. 具有n个结点的完全二叉树的深度为log2(n)+1

# 代码实现

## 向量实现
https://blog.csdn.net/weixin_42100963/article/details/103639782

以层序遍历在数组种存储


```C++
void CMyTreeArr<T>::prePrint(int index)
{
    // 限制范围
    if(index < vecBuff.size() && index >= 0)
    {
        cout << vecBuff[index] << " ";	// 根
        // 数组下标的方式	   递归调用  找到计算规律	文章底部将 画图演示 
        prePrint(2 * index + 1);	// 左子树 == 根结点 * 2 + 1
        prePrint(2 * index + 2);	// 右子树 == 根结点 * 2 + 2
    }
}
template<typename T>
inline void CMyTreeArr<T>::inPrint(int index)
{
    if(index < vecBuff.size() && index >= 0)
    {
        inPrint(2 * index + 1);
        cout << vecBuff[index] << " ";	// 根
        inPrint(2 * index + 2);		
    }
}

template<typename T>
inline void CMyTreeArr<T>::posPrint(int index)
{
    if(index < vecBuff.size() && index >= 0)
    {
        inPrint(2 * index + 1);
        inPrint(2 * index + 2);
        cout << vecBuff[index] << " ";
    }
}

template<typename T>
inline void CMyTreeArr<T>::levlPrint()
{
    for(auto i : vecBuff)	// 直接输入 vecBuff中的元素
    { 
        cout << i << " ";
    }
}
```



## 链表实现

前中后序非递归
https://blog.csdn.net/weixin_45599288/article/details/122345321



```C++
#include<bits/stdc++.h>

using namespace std;

template<typename DataType> 
struct BiNode
{
    DataType data;
    BiNode<DataType>*lchild, *rchild;
};

template<typename DataType> 
class BiTree{
public:
    BiTree(){root = Creat();}
    BiTree(BiTree<DataType>* b){
        root = Copy(b->root);
    }
    ~BiTree(){Release(root);}
    void PreOrder(){PreOrder(root);}
    void InOrder(){InOrder(root);}
    void PostOrder(){PostOrder(root);}
    int Leaf_count(){
        int ans =  Leaf_count(root);
        return ans;
    }
    int Node_count(){
        int ans = Node_count(root);
        return ans;
    }
    int Deep(){
        int ans = Deep(root);
        return ans;
    }

    void Judge_sort(){
        if(Judge_sort(root)){
            cout << "ture";
        }
        else{
            cout << "fales";
        }
    }
    void Find_bro(DataType x){
        find_bro(root,x);
    }
    bool Empty(){
        if(root == nullptr){
            return false;
        }
        else{
            return true;
        }
    }
    void insert(DataType insert_data, DataType step_data){
        insert(root,insert_data, step_data);
    }
    void LevelOrder();//层序遍历

private:
    int flag = 0;
    BiNode<DataType>* root;
    BiNode<DataType>* Creat();
    BiNode<DataType>* Copy(BiNode<DataType>* node);
    int Leaf_count(BiNode<DataType>* node);//计算叶子结点数
    int Node_count(BiNode<DataType>* node);//计算结点数
    int Deep(BiNode<DataType>* node);//计算深度
    void Release(BiNode<DataType>* node);//析构函数
    void PreOrder(BiNode<DataType>* node);//前序遍历
    void InOrder(BiNode<DataType>* node);//中序遍历
    void PostOrder(BiNode<DataType>* node);//后序遍历
    void find_bro(BiNode<DataType>* node,DataType x);
    bool Judge_sort(BiNode<DataType>* node);
    
    void inorDer();//非递归遍历
    void insert(BiNode<DataType>* root, DataType insert_data, DataType step_data);//在指定值之后插入
};

template<typename DataType> 
BiNode<DataType>* BiTree<DataType>::Creat(){
    BiNode<DataType>* node;
    char cin_data;
    cin >> cin_data;
    //cin_data = my_data[i++];
    if(cin_data=='#'){
        node = nullptr;
    }
    else{
        node = new BiNode<DataType>;
        node->data = cin_data;
        node->lchild = Creat();//左递归建造子树
        node->rchild = Creat();//右递归建造子树
    }
    return node;
}

template<typename DataType> 
BiNode<DataType>* BiTree<DataType>::Copy(BiNode<DataType>* node){
    if(node == nullptr){
        return nullptr;
    }
    BiNode<DataType>* copy_node ;
    copy_node->data = node->data;
    copy_node->lchild = Copy(node->lchild);
    copy_node->rchild = Copy(node->rchild);
    return copy_node;

}

template<typename DataType> 
int BiTree<DataType>::Leaf_count(BiNode<DataType>* node){
    int count ;
    if(node == nullptr){
        count = 0;
    }
    else if(node->lchild == nullptr && node->rchild == nullptr){
        count = 1;
    }
    else{
        count = Leaf_count(node->lchild) + Leaf_count(node->rchild);
    }
    return count;
}

template<typename DataType> 
int BiTree<DataType>::Node_count(BiNode<DataType>* node){
    int count ;
    if(node == nullptr) count = 0;
    else{
        count = Node_count(node->lchild) + Node_count(node->rchild) +1;
    }
    return count;
}

template<typename DataType>
int BiTree<DataType>::Deep(BiNode<DataType>* node){
    int deep=0;
    if(node)
    {
        int leftdeep=Deep(node->lchild);
        int rightdeep=Deep(node->rchild);
        deep = leftdeep>=rightdeep?leftdeep+1:rightdeep+1;
    }
    return deep;
}

template<typename DataType> 
void BiTree<DataType>::Release(BiNode<DataType>* node){
    if(node == nullptr) return;
    else{
        Release(node->lchild);
        Release(node->rchild);
        delete node;
    }
}

template<typename DataType> 
void BiTree<DataType>::PreOrder(BiNode<DataType>* node){
    if(node == nullptr) return;
    else{
        cout << node->data<<' ';
        PreOrder(node->lchild);
        PreOrder(node->rchild);
    }
}

template<typename DataType> 
void BiTree<DataType>::InOrder(BiNode<DataType>* node){
    if(node == nullptr) return;
    else{
        
        InOrder(node->lchild);
        cout << node->data<<' ';
        InOrder(node->rchild);
    }
}

template<typename DataType> 
void BiTree<DataType>::PostOrder(BiNode<DataType>* node){
    if(node == nullptr) return;
    else{
        
        PostOrder(node->lchild);
        PostOrder(node->rchild);
        cout << node->data<<' ';
    }
}

template<typename DataType> 
bool BiTree<DataType>::Judge_sort(BiNode<DataType>* node){
     if(!node || (!(node->lchild)&&!(node->rchild)))             
        return true;
    else if((node->lchild)&&!(node->rchild)){  
        if(node->lchild->data>node->data)
            return false;
        else
            return Judge_sort(node->lchild);
    }
    else if((node->rchild)&&!(node->lchild)){  
        if(node->rchild->data<node->data)
            return false;
        else
            return Judge_sort(node->rchild);
    }
    else{                           
        if((node->lchild->data > node->data) || (node->rchild->data < node->data))
            return false;
        else
            return (Judge_sort(node->lchild) && Judge_sort(node->rchild));
    }
}

template<typename DataType> 
void BiTree<DataType>::find_bro(BiNode<DataType>* node,DataType x){
    if(node == nullptr) return;
    else{
        if(node->lchild!=nullptr&&node->rchild!=nullptr){
            if(node->lchild->data==x){
                BiNode<DataType>* r = node->rchild;
                cout << r->data << "---"<<r << endl;
            }
            else if(node->rchild->data==x){
               BiNode<DataType>* l = node->lchild;
                cout << l->data << "---"<<l <<endl;
            }
        }
        find_bro(node->lchild,x);
        find_bro(node->rchild,x);
    }
}

template<typename DataType>
void BiTree<DataType>::LevelOrder(){
	BiNode<DataType>*Q[100],*q=nullptr;
	int front = -1,rear = -1;
	if(root == nullptr)return;
	Q[++rear] = root;
	while(front!=rear){
		q = Q[++front];
		cout<<q->data<<" ";
		if(q->lchild != nullptr) Q[++rear] = q->lchild;
		if(q->rchild != nullptr) Q[++rear] = q->rchild;
	}
}

template<typename DataType>
void BiTree<DataType>::inorDer(){
	if(root != nullptr){
		stack<BiNode<DataType>*> s;
		BiNode<DataType>*p = root;
		while(!s.empty() || p !=nullptr){
			while( p!= nullptr){
				s.push(p);
				p = p->lchild;
			}
			if(!s.Empty()){
				p = s.pop();
				cout << p->data;
				p = p->rchild;
			}
		}
	}
}

template<typename DataType>
void BiTree<DataType>::insert(BiNode<DataType>* node, DataType insert_data, DataType step_data){
        if(node == nullptr) return;
    else{
        if(node->data == step_data){
            BiNode<DataType>* node1;
            BiNode<DataType>* node2;
            //cout << 233;
            node1 = node->lchild;
            
            node2->data = insert_data;
            node2->lchild = node1;
            node2->rchild = nullptr;
            node->lchild = node2;
            
           
            //return;
        }
        //cout << node->data<<' ';
        insert(node->lchild,insert_data,step_data);
        insert(node->rchild,insert_data,step_data);
    }
}
```









# 森林/二叉树互换

## 树 ->二叉树
1. 加线
在所有兄弟间加连线
2. 去线
对树中每个结点，保留它与第一个孩子结点的连线
3. 层次调整
<a href="https://sm.ms/image/zSFrsZubHTy3gk6" target="_blank"><img src="https://s2.loli.net/2021/12/15/zSFrsZubHTy3gk6.jpg" ></a>

## 二叉树 ->树
1. 加线
若某结点左孩子存在，将次左孩子的n个右孩子结点等作为此结点的孩子连线
2. 去线
删除原二叉树中所有结点与其右孩子的连线
3. 调整层次
<a href="https://sm.ms/image/XxcBefKZyNmoE81" target="_blank"><img src="https://s2.loli.net/2021/12/15/XxcBefKZyNmoE81.jpg" ></a>

## 森林 -> 二叉树
1. 将每个树转化为二叉树  

2. 第一棵二叉树不动，从第二棵开始，依次把后一棵二叉树的根节点作为前一棵二叉树根节点的右孩子，连接
<a href="https://sm.ms/image/RdUKizQjAZrnMph" target="_blank"><img src="https://s2.loli.net/2021/12/15/RdUKizQjAZrnMph.jpg" ></a>


## 二叉树 -> 森林
1. 从根节点开始若右孩子存在，则将其与右孩子的连线删除。 

2. 对每一个分离后的二叉树，重复步骤1

3. 再将分离后的二叉树转为树
<a href="https://sm.ms/image/zqXHDlR62ZY5xiV" target="_blank"><img src="https://s2.loli.net/2021/12/15/zqXHDlR62ZY5xiV.jpg" ></a>

# 二叉排序树

## 定义
一棵空树，或者是具有下列性质的二叉树：
1. 若左子树不空，则左子树上所有结点的值均小于它的根结点的值；
2. 若右子树不空，则右子树上所有结点的值均大于它的根结点的值；
3. 左、右子树也分别为二叉排序树；
4. 没有键值相等的结点。

<img src="https://bkimg.cdn.bcebos.com/pic/94cad1c8a786c9179df9bed6c93d70cf3ac75763?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2U4MA==,g_7,xp_5,yp_5/format,f_auto" alt="" style="width:100%" />  

## 查找

### 步骤：
1. 若根结点的关键字值等于查找的关键字，成功。
2. 否则，若小于根结点的关键字值，递归查左子树。
3. 若大于根结点的关键字值，递归查右子树。
4. 若子树为空，查找不成功。

### 性能分析
每个结点的C(i)为该结点的层次数。最坏情况下，当先后插入的关键字有序时，构成的二叉排序树蜕变为单支树，树的深度为其平均查找长度(n+1)/2(和顺序查找相同），最好的情况是二叉排序树的形态和折半查找的判定树相同，其平均查找长度和log 2 (n)成正比。
也就是说，最好情况下的算法时间复杂度为O(1)，最坏情况下的算法时间复杂度为O(n)。

# 平衡二叉树

## 定义
平衡二叉查找树：简称平衡二叉树。由前苏联的数学家 Adelse-Velskil 和 Landis 在 1962 年提出的高度平衡的二叉树，根据科学家的英文名也称为 AVL 树。它具有如下几个性质：

1. 可以是空树。
2. 假如不是空树，任何一个结点的左子树与右子树都是平衡二叉树，并且高度之差的绝对值不超过 1。

## 平衡二叉树调整
引用：
https://www.cnblogs.com/zhangbaochong/p/5164994.html

1. 单旋转
<img src="https://images2015.cnblogs.com/blog/805461/201601/805461-20160127220751410-639565779.jpg" alt="" style="width:100%" /> 
k2结点不满足平衡性，它的左子树k1比右子树z深两层，k1子树中更深的是k1的左子树x，因此属于左左情况。

为了恢复平衡，我们把x上移一层，并把z下移一层，但此时实际已经超出了AVL树的性质要求。为此，重新安排结点以形成一颗等价的树。为使树恢复平衡，我们把k2变成这棵树的根节点，因为k2大于k1，把k2置于k1的右子树上，而原本在k1右子树的Y大于k1，小于k2，就把Y置于k2的左子树上，这样既满足了二叉查找树的性质，又满足了平衡二叉树的性质。


2. 双旋转
<img src="https://images2015.cnblogs.com/blog/805461/201601/805461-20160127221858707-881408395.jpg" alt="" style="width:100%" /> 
对于上图情况，为使树恢复平衡，我们需要进行两步，第一步，把k1作为根，进行一次右右旋转，旋转之后就变成了左左情况，所以第二步再进行一次左左旋转，最后得到了一棵以k2为根的平衡二叉树。


# 最大二叉树

## 例题

给定一个不含重复元素的整数数组 nums 。一个以此数组直接递归构建的 最大二叉树 定义如下：

1. 二叉树的根是数组 nums 中的最大元素。
2. 左子树是通过数组中 最大值左边部分 递归构造出的最大二叉树。
3. 右子树是通过数组中 最大值右边部分 递归构造出的最大二叉树。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-binary-tree


<img src="https://img-blog.csdnimg.cn/20210612003134409.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80ODI3NjI5OA==,size_16,color_FFFFFF,t_70>" alt="" style="width:100%" /> 


## 代码实现
{% codeblock [最大二叉树] [lang:C++]  %}
void max_BiTree(int first,int max_index,int last){
    int max_l = first,max_r = last-1;
    if(first == last){
        return;
    }
    for(int i=first;i<max_index;i++){
        if(arr1[i]>arr1[max_l]){
            max_l = i;
        }
    }
    for(int j=max_index+1;j<last;j++){
        if(arr1[j]>arr1[max_r]){
            max_r = j;
        }
    }
    cout << arr1[max_index]<<' ';
    max_BiTree(first,max_l,max_index);
    max_BiTree(max_index+1,max_r,last);
}
{% endcodeblock %}

# 哈夫曼树

## 定义与原理
给定N个权值作为N个叶子结点，构造一棵二叉树，若该树的带权路径长度达到最小，称这样的二叉树为最优二叉树，也称为哈夫曼树(Huffman Tree)。哈夫曼树是带权路径长度最短的树，权值较大的结点离根较近。

参考博客：
http://c.biancheng.net/view/3398.html
https://blog.csdn.net/Mr_GYF/article/details/121707714?utm_source=app&app_version=4.20.0
## 哈夫曼编码

# 

<hr />
版权信息