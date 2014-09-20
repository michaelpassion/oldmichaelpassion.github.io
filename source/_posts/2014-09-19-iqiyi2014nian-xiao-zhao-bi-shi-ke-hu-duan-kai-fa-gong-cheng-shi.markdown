---
layout: post
title: "iqiyi2014年校招笔试 客户端开发工程师"
date: 2014-09-19 20:38:30 +0800
comments: true
categories: 面试 笔试 
---
![](http://campus.iqiyi.com/html/images/index/logo.png)   
先总结一下：考的内容比较基础，概率题不难，排序题不难，语法细节的题目较少，后面大题没有算法题，都是概念性的问题，复习的好的话应该不是问题，问题是我没有复习好~~~~(>_<)~~~~。
<!--more-->
1. 在C和C++中，申请和释放内存的基本操作是什么，它们之间区别是什么？  
	___

    C语言提供内存动态分配的函数有：malloc、calloc、realloc，在使用这些念书时必须包含其头文件，分别为：`<malloc.h>,<stdlib.h>,<alloc.h> ` 
	* malloc 函数： `void *malloc(unsigned int size)`
	在内存的动态分配区域中分配一个长度为size的连续空间。如果分配成功，则返回所分配内存空间的首地址，否则返回NULL，申请的内存不会进行初始化。“类型说明符”表示把该区域用于任何数据类型。（类型说明符 *）表示吧返回值强制转换为该类型的指针。 “size”是一个无符号数。
	* calloc 函数：`void *calloc(unsigned int num, unsigned int size)`  
	按照所给的数据古树和数据类型所占字节数，分配一个num * size连续的空间。函数返回该存储区的其实地址。calloc函数与malloc函数的区别仅在于一次可以分配n块区域。例如 `ps=(struct stu *) calloc(2,sizeof (struct stu))`; 其中的`sizeof(struct stu)`是求stu的结构长度。因此该语句的意思是：按stu的长度分配2块连续区域，强制转换为stu类型，并把其首地址赋予指针变量ps。
	* realloc 函数：`void *realloc(void *ptr, unsigned int size)`   
	重新定义所开辟内存的空间的大小。其中ptr所指的内存空间是签署函数已经开辟的，size为新的空间大小，其值可比原来大或小。函数返回新存储区的起始地址（该地址可能与以前的地址不同）。例如p1=(float *)realloc(p1,16);将原先开辟的8个字节调整为16个字节。  
**动态申请的内存空间要进行手动用free（）函数释放**  
	* free 函数 `void free(void *ptr)`  
	将以前开辟的某内存空间释放，其中`ptr`为存放待释放空间起始地址的指针变量，函数无返回值。应注意：`ptr`指向需要释放的内存空间的首地址  
	**C++**  
	在C++中，内存分为5个区，分别是堆，栈，自由存储区，全局/静态存储区，和常量存储区。  
	申请和释放堆中分诶的存储空间，分别使用new 和 delete 两个运算符来完成。  
	对于非内部数据类型对象而言，光用malloc/free无法满足动态对象的要求。对象在创建的同时要自动执行构造函数，对象在消亡之前要自动执行析构函数。由于malloc/free是库函数而不是运算符，不在编译器控制权限之内，不能够把执行构造函数和析构函数的任务强加于malloc/free.  
	
	
	
	
2. 分析采用线性表，二叉平衡树和哈希表存储数据的优劣。
* * *  
   线性表分为顺序存储结构和链式存储结构，顺序存储结构的有点事可以实现随机读取，时间复杂度O(1)，空间利用率高；缺点是进行插入杀出操作时需要移动大量数据，时间复杂度为O(n),同时容量受限制，需要事先去顶容量大小，容量大浪费空间资源，过小产生溢出。链式存储结构有点，插入和删除非常简单，前提条件是知道要插入的位置，时间复杂度为O(1),但如果如果不知道插入位置，定位需要遍历链表，时间复杂度为O(n),优点是没有容量限制，可以在使用过程中动态分配内存，缺点是不能实现随机读取，空间利用率低。  
二叉平衡树 的查找效率为O(logn),插入删除也是O(logn)，缺点是需要额外的指针空间。  
哈希表O(1)时间做查找，插入和删除，时间复杂度为O(n)。    
	
3. strcpy是字符串拷贝函数，原型是`char *strcpy(char *strDest, const char *strSrc);`  
1) 请实现函数strcpy  
2）strcpy能把strSrc的内容复制到StrDest，为什么还要 `char*`类型的返回值
*** 
1） 代码如下：需要注意的点:
* 检查指针的有效性，古国检查指针的有效性使用`((!strDes）&& (!strSrc))`,说明对C语言中类型的隐式转换没有深刻认识`(!strDest)`是将`char*`转换成bool即是类型隐式转换
```c++
	char *strcpy(char *strDest, const char *strSrc)
	{
		assert((strDest != NULL) && (strSrc != NULL));
		char *address = strDest;
		while(*strSrc != '/0')
			*strDest++ = *strSrc++; 			
		*++strDest = '/0';
		return address;
	}
	
	char *strcpy(char *strDest, const char *strSrc)
	{
		assert((strDest != NULL) && (strSrc != NULL));
		char *address = strDest;
		while(*strSrc != '/0')
			*strDest++ = *strSrc++; 			
		*++strDest = '/0';
		return address;
	}
```
   
2) 返回 `char*`的指针是为了实现链式表达式。


	
 