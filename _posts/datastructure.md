---
title: Linary DataStructure
author: Wu Han
date: 2020-10-15 22:54:00 +0800
categories: [Coding, C/C++]
tags: [DataStructure]
toc: true
math: true
---

## 算法
- 有输入输出 明确 可持续 有限性 
- 算法的复杂度
    - 存储复杂度
    - 时间复杂度(抽象为基本操作次数)
    > O: def 相同数量级 $lim(n->\infin)\frac{f(n)}{g(n)}= a$
    >即$f(n) = O(g(n))$

# 第二章 线性结构

#### 何为线性结构 
>有序或者无序的集合
>线性结构的运算(交，并.etc)

#### Part 1 线性结构的常用操作 完成集合运算
* initlist()//创建线性结构
* destroylist()//销毁线性结构
* clearlist()//清空线性结构内容
* listlength()//求线性结构元素个数（长度）
* getelement()//从线性结构读取某元素
* listempty()//判断线性结构是否为空
* priorelement()//求线性结构前驱元素
* nextelement()//求线性结构后继元素
* listinsert()//向线性结构里插入元素
* listdelete()//删除线性结构里的某元素
* listtravers()//遍历线性结构的元素
* locateitem()//返回线性结构里某元素的第一个位置

> eg: A∪B 
思路:依次从a中取出元素插入c中,再将b中元素插入c中(可以在插入之前判断c中是否有相同元素)


```c
void Union(List a,List b, List c){
    for (int i=0;i=getlen();i++){
        int x = getelement();
        //if (!locateitem(x)){
        listinsert(x);
        //}
    }
    for(...){
        ...
    }
}
```
#### Part 2 线性结构的表示方法之一(数组)
```C
#define MAXNUM 1000
typedef struct{
    Element a[MAXNUM]
    int Listsize;
    int Listlength
}SLIST;//static
DLIST //动态
```

```c
#define LIST_INIT_SIZE 100
#define LIST_INC_SIZE 20
typedef struct{
    ElemType *elem;
    int listsize;
    int length;
}SqList;//ElemType 是一种数据结构类型 按需要替换
```

```c
void InitList_sq(SqList &L,int msize = LIST_INIT_SIZE)
{
    L.elem = nem ElemType[msize];
    L.listsize = msize;
    L.length = 0;
}
```

```C
void DestoryList_sq(SqList &L){
    delete [] L.elem;
    L.length = 0;
    L.listsize = 0;
}
```

```C
bool ListEmpty_sq(SqList L){
    return (L.length == 0);
}
```
```C
bool ListFull_sq(SqList L){
    return (L.length == L.listsize);
}
```
```c
int ListLength_sq(SqList L){
    return L.length;
}
```
```c
int LocateItem_sq(SqList L,Elemtype e){
    for(int i=1;i<=L.length;i++){
        if(L.elem[i-1] == e)return i;
    return 0;
    }
}
```
```C
void GetItem_sq(SqList L,int i,Elemtype &e){
    e = L.elem[i-1];
}
```
```C
void ListInsert_sq(SqList &L,int i,Elemtype e){
    if (i<1||i>L.length+1){ErrorMsg("i 值非法!");return;}
    if(L.length == L.listsize)Increment(L);
    for (j = L.length -1;j>=i-1;j--){
        L.elem[j+1] = L.elem[j];
    }
    L.elem[i-1] = e;
    ++ L.length;
}
```
```c
void Increment(SqList &L,int inc_size = LIST_INC_SIZE){
    Elemtype a*;
    a = new Elemtype[L.listsize+inc_size];
    if(!a){ErrorMsg("内存分配错误！");return;}
    for(i=0,i<L.length;i++)a[i] = L.elem[i];
    delete [] L.elem;
    L.elem = a;
    L.listsize += inc_size;
}
```
```C
void ListDelete_sq(SqList &L,int i,Elemtype &e){
    if(i<1||i>L.length){ErrorMsg("i值非法！");return;}
    e = L.elem[i-1];
    for (j = i;j<L.length-1;j++)
        L.elem[j-1] = L.elem[j];
    L.length --;
}
```
#### Part 3 线性结构的常用操作实现

#### Part 4 线性结构的表示方法之二(指针)

#### Part 5 线性结构的常用操作实现

>9.22 作业:
A∩B -> C (advance:放入B)
A异或B -> C(advance:放入B)