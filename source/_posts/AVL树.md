---
title: 平衡二叉树详解
tags:
	- AVL
	- 查找
copyright: true
date: 2021-12-15 17:12:03
permalink:
categories:

	- 算法
description:

image:
---

**前言**

总结一下平衡二叉树 AVL树的一些用法和代码

引用文章：
https://www.cnblogs.com/wasi-991017/p/13824039.html

<a href="https://sm.ms/image/Ag1Owom6QxB5c2s" target="_blank"><img src="https://s2.loli.net/2021/12/15/Ag1Owom6QxB5c2s.jpg" alt="RL.jpg"></a>

<!-- more -->

# 基本概念

平衡二叉树可以理解为是二叉排序树的优化版本，在二叉排序树的应用过程中会出现子树间深度差距大而导致查找性能下降的情况，所以就有了平衡二叉树这种优化方法。

可以得出平衡二叉树的定义

1. 基于二叉排序树

2. 左右子树的深度之差的绝对值不超过1

3. 左右子树都是平衡二叉树

定义平衡因子为本根节点的 左子树深度 - 右子树深度

# 关键部分 ———— 调整方法

## LL型
左子树平衡因子 大于 右子树 且 左子树的左子树平衡因子 大于 左子树的右子树平衡因子 ——两个子树也可用
<img src="https://s2.loli.net/2021/12/15/QKY3xkvubPqNjgJ.jpg" alt="" style="width:100%" /> 

## RR型
右子树平衡因子 大于 左子树 且 右子树的右子树平衡因子 大于 右子树的左子树——两个子树也可用
<a href="https://sm.ms/image/lZ15qnmcpzQ7uM4" target="_blank"><img src="https://s2.loli.net/2021/12/15/lZ15qnmcpzQ7uM4.jpg" alt="RR.jpg"></a> 

## LR型
左子树平衡因子 大于 右子树 且 左子树的右子树平衡因子 大于 左子树的左子树
<a href="https://sm.ms/image/nOhJW9jx7ARqTlu" target="_blank"><img src="https://s2.loli.net/2021/12/15/nOhJW9jx7ARqTlu.jpg" alt="LR.jpg"></a>


## RL型
右子树平衡因子 大于 左子树 且 右子树的左子树平衡因子 大于 右子树的右子树
<a href="https://sm.ms/image/Ag1Owom6QxB5c2s" target="_blank"><img src="https://s2.loli.net/2021/12/15/Ag1Owom6QxB5c2s.jpg" alt="RL.jpg"></a>
# 代码实现
转自：https://www.cnblogs.com/wasi-991017/p/13824039.html

## 笔记
124 - 142 排序二叉树的插入操作 插入后做平衡操作者
209 - 230 平衡操作 判断情况并调用不同情况函数 LL RR LR RL
237 - 271 不同情况对应函数
注意旋转操作和插入操作都返回一个根节点(学习！！！)
eg：
subRoot->rChild = Insert(subRoot->rChild, k);


BalanceFactor() 返回某结点的平衡因子

## 完整代码
{% codeblock [xxxxxx] [lang:]  %}
/*******平衡二叉树（AVL）***********/
#pragma once
#include<iostream>
using namespace std;

///平衡二叉树结点结构
struct AVLNode {
	int data;
	AVLNode *lChild, *rChild;
	AVLNode(int a) {
		data = a;
		lChild = NULL;
		rChild = NULL;
	}
};

class AVLTree {
public:
	AVLTree() {
		root = NULL;
	}
	~AVLTree() {
		destroy(root);
	}

	///从命令行接受数据创建AVL树。使用其他方式创建原理一致
	void Create() {
		cout << "input numbers to create AVL: " << endl;
		int temp;
		while (cin >> temp) {
			root=Insert(root, temp);
		}
		cout << "AVL创建完成！" << endl;
		Print();
	}

	///返回某结点为根节点的子树高度
	int Height(AVLNode *p) {
		if (p == NULL)
			return 0;
		int i = Height(p->lChild);
		int j = Height(p->rChild);
		return i > j ? i + 1 : j + 1;
	}

	///输出该排序树
	void Print() {
		cout << "中序遍历为： ";
		MidOrder(root);
		cout << endl;
		cout << "先序遍历为： ";
		PreOrder(root);
		cout << endl;
	}

	///先序遍历输出
	void PreOrder(AVLNode *p) {
		if (p != NULL) {
			cout << p->data << " ";
			PreOrder(p->lChild);
			PreOrder(p->rChild);
		}
	}
	///中序遍历输出
	void MidOrder(AVLNode *p) {
		if (p != NULL) {
			MidOrder(p->lChild);
			cout << p->data << " ";
			MidOrder(p->rChild);
		}
	}

	///简化版插入函数
	void Insert(const int x) {
		root = Insert(root, x);
	}

	///简化版删除函数
	void Remove(int x) {
		root=Remove(root, x);
	}

	///返回值为x的结点指针
	AVLNode* Search(int x) {
		AVLNode *p = root;
		while (p) {
			if (p->data == x)
				break;
			else if (p->data < x)
				p = p->rChild;
			else
				p = p->lChild;
		}
		return p;
	}

	///返回子树最大值结点的指针
	AVLNode* TreeMax(AVLNode* subTree) {
		if (!subTree)
			return NULL;
		while (subTree->rChild) {
			subTree = subTree->rChild;
		}
		return subTree;
	}

	///返回子树最小值结点的指针
	AVLNode* TreeMin(AVLNode* subTree) {
		if (!subTree)
			return NULL;
		while (subTree->lChild) {
			subTree = subTree->lChild;
		}
		return subTree;
	}

private:
	///根节点
	AVLNode *root;

	///插入（视为在某结点为根节点的子树上进行插入）
	//对子树上进行插入操作后都需要平衡操作，可能会改变该子树的根节点，
	//因此设置返回值记录完成操作后子树的根结点指针)
	AVLNode* Insert(AVLNode* subRoot, const int k) {
		if (subRoot == NULL) {
			subRoot = new AVLNode(k);
		}
		else if (k > subRoot->data) //需要在右子树上插入新的结点
		{
			subRoot->rChild = Insert(subRoot->rChild, k);
			//在右子树上插入结点后可能导致不平衡，故需要对右子树进行平衡操作
			//而平衡操作可能会导致子树根结点产生变化，故需更新当前的子树根节点
			subRoot = Balancee(subRoot);
		}
		else if (k < subRoot->data) { //需要在左子树上插入新的结点
			subRoot->lChild = Insert(subRoot->lChild, k);
			//和上面同理
			subRoot = Balancee(subRoot);
		}
		//将新的子树根结点指针返回供原父节点更新孩子指针
		return subRoot;
	}

	///删除结点（视为在该结点为根节点的树上进行删除操作）
	AVLNode* Remove(AVLNode* subRoot, int x) {
		if (!Search(x)) {//不存在x的结点则直接返回
			cout << "不存在值为" << x << "的结点！" << endl;
			return root;
		}

		if (!root)  //root为空指针都直接返回NULL
			return root;

		if (subRoot->data == x)  //情况1：要删除的就是该树的根节点
		{
			if (subRoot->lChild && subRoot->rChild)//情况1.1：该树的左右子树都存在
			{
				if (BalanceFactor(subRoot)>0) 
				{
					//左子树高于右子树，则根节点的值替换为其直接前驱的值，然后转化为删除
					//其直接前驱(其位于左子树上，也就意味着去降低左子树高度)
					AVLNode *tmp = TreeMax(subRoot->lChild); //直接前驱就是左子树的最大值
					subRoot->data = tmp->data;
					//递归调用Remove()删除subRoot的左子树上的前驱结点后，Remove()返回可能为
					//新的subRoot的左子树根节点供subRoot更新左孩子结点((Remove()会调用Balance()函数平衡其操作的树))。
					subRoot->lChild = Remove(subRoot->lChild, tmp->data);
				}
				else {
					//右子树高于左子树，则根节点的值替换为其直接后继的值，
					//然后转化为删除其直接后继(其位于右子树上，也就意味着去降低右子树高度)
					AVLNode *tmp = TreeMin(subRoot->rChild);
					subRoot->data = tmp->data;
					subRoot->rChild = Remove(subRoot->rChild, tmp->data);
				}
			}
			else //情况1.2：只存在一颗子树或者都不存在
			{
				//直接将根节点更新为其孩子结点(都不存在则为NULL)
				AVLNode * tmp = subRoot;
				subRoot = (subRoot->lChild) ? (subRoot->lChild) : (subRoot->rChild);
				delete tmp;
				tmp = NULL;
			}
		}
		else if (x < subRoot->data) { //情况2：要删除的节点位于左子树上
			//递归调用,在subRoot的左子树上进行删除操作，并返回新的左子树根节点供subRoot更新左孩子指针
			subRoot->lChild = Remove(subRoot->lChild, x);
			//在subRoot的左子树上完成删除操作后,可能导致该树不平衡,故需要进行平衡操作并更新当前根节点
			if (BalanceFactor(subRoot) < -1)
				subRoot = Balancee(root);
		}
		else {//情况3：要删除的节点位于右子树上
			//递归调用,在subRoot的右子树上进行删除操作，并返回新的右子树根节点供subRoot更新右孩子指针
			subRoot->rChild = Remove(subRoot->rChild, x);
			//在subRoot的右子树上完成删除操作后,可能导致该树不平衡,故需要进行平衡操作并更新当前根节点
			if (BalanceFactor(subRoot) >1)
				subRoot = Balancee(subRoot);
		}
		//返回该树当前根节点供其父节点更新孩子节点
		return subRoot;
	}

	///返回某个节点的平衡因子
	int BalanceFactor(AVLNode *p) {
		return Height(p->lChild) - Height(p->rChild);
	}

	///对某个结点进行平衡操作（根据平衡因子调用四种不同的旋转操作）
	AVLNode* Balancee(AVLNode* subRoot) {
		int bf = BalanceFactor(subRoot);
		if (bf > 1) //左子树更高
		{
			if (BalanceFactor(subRoot->lChild) > 0)
				//左孩子结点平衡因子>0说明新节点多在了左子树上，因此调用LL_Rotation
				subRoot = LL_Rotation(subRoot);
			else
				//左孩子结点平衡因子<0说明新节点多在了右子树上，因此调用LR_Rotation
				subRoot = LR_Rotation(subRoot);
		}
		else if (bf < -1) //右子树更高
		{
			if (BalanceFactor(subRoot->rChild) > 0)
		        //右孩子结点平衡因子>0说明新节点多在了左子树上，因此调用RL_Rotation
				subRoot = RL_Rotation(subRoot);
			else
			    //右孩子结点平衡因子<0说明新节点多在了右子树上上，因此调用RR_Rotation
				subRoot = RR_Rotation(subRoot);
		}
		//对分支结点进行平衡操作后可能会更新该分支节点，故将新的分支结点返回供原父结点更新孩子指针
		return subRoot;
	}
	/*****************************
	          四种旋转操作
	******************************/
	/// LL平衡旋转(右单旋转)
	//在左孩子(L)的左子树(L)上插入导致不平衡，需要向右旋转一次实现平衡
	AVLNode* LL_Rotation(AVLNode *subRoot) {
		AVLNode* temp = subRoot->lChild;
		subRoot->lChild = temp->rChild;
		temp->rChild = subRoot;
		//完成旋转操作之后，该处分支结点(原为subRoot)发生了变化，
		//因此要返回新的分支节点指针供其父节点更新孩子指针
		return temp;
	}
	/// RR平衡旋转(左单旋转)
	//在右孩子(R)的右子树(R)上插入导致不平衡，需要向左旋转一次实现平衡
	AVLNode* RR_Rotation(AVLNode *subRoot) {
		AVLNode* temp = subRoot->rChild;
		subRoot->rChild = temp->lChild;
		temp->lChild = subRoot;
		//完成旋转操作之后，该处分支结点(原为subRoot)发生了变化，
		//因此要返回新的分支节点指针供其父节点更新孩子指针
		return temp;
	}
	/***********下面两种情况可看作是对根节点和子节点进行上两种旋转操作的组合*****************/
	/// RL平衡旋转(先右后左双旋转)
	//在右孩子(R)的左子树(L)上插入导致不平衡，需要先对分支结点的右孩子进行一次右旋(LL_Rotation),
	//再对分支结点进行一次左旋(RR_Rotation)
	AVLNode* RL_Rotation(AVLNode *subRoot) {
		//对subRoot右孩子结点LL旋转后，更新subRoot右结点指针
		subRoot->rChild=LL_Rotation(subRoot->rChild);  
		return RR_Rotation(subRoot);//返回新的分支结点供原分支节点的父节点更新孩子指针
	}
	/// LR平衡旋转(先左后右双旋转)
	//在左孩子(L)的右子树(R)上插入导致不平衡,需要先对分支结点的左孩子进行一次左旋(RR_Rotation),
	//再对分支结点进行一次右旋(LL_Rotation)
	AVLNode* LR_Rotation(AVLNode *subRoot) {
		//对subRoot左结点RR旋转后，更新subRoot左结点指针
		subRoot-> lChild = RR_Rotation(subRoot->lChild);  
		return LL_Rotation(subRoot);//返回新的分支结点供原分支节点的父节点更新孩子指针
	}

	///销毁该树
	void destroy(AVLNode* p) {
		if (p) {
			destroy(p->lChild);
			destroy(p->rChild);
			delete p;
		}
	}
};
{% endcodeblock %}
<hr />
版权信息