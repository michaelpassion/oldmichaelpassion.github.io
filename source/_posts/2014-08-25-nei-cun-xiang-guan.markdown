---
layout: post
title: "内存相关"
date: 2014-08-25 22:24:17 +0800
comments: true
categories: 基础知识 c++
---
###1. 内存对齐：  
 编译器会自动进行成员变量的对齐，以提高运算效率。缺省情况下，编译器为结构体的每个成员按其自然对界（natural alignment）条件分配内存。每个成员按照它们被声明的顺序在内存中存储，第一个成员的地址和整个结构体的地址相同。  
 为什么要进行内存对齐呢，原因在于，为了访问未对齐的内存，处理器需要作两次内存访问；然而，对齐的内存访问仅需要一次访问。所以为了内存的有效利用，我们有必要在定义结构体前考虑下成员的顺序。字，双字，和四字在自然边界上不需要在内存中对齐。（对字，双字，和四字来说，自然边界分别是偶数地址，可以被4 整除的地址，和可以被8 整除的地址。）
 除此之外我们还可以利用#pragma pack（）来改变编译器的默认对齐方式。使用伪指令#pragma pack (n)，编译器将按照n个字节对齐；使用伪指令#pragma pack ()，取消自定义字节对齐方式。注意：如果
/#pragma pack (n)中指定的n大于结构体中最大成员的size，则其不起作用，结构体仍然按照size最大的成员进行对界。其对齐的规则是,每个成员按其类型的对齐参数(通常是这个类型的大小)和指定对齐参数
(这里是n 字节)中较小的一个对齐，即：min( n, sizeof( item ))
###2. struct与class的区别:
在C++中，struct与class的区别有两点，一是struct中成员变量和函数的默认访问权限为public，而class的为private。二是由于C++中struct兼容了C中的struct的所有特性，可以定义的时候直接
以{ }对其成员变量赋初值，而class则不能。

###cpu与外设之间的数据传送方式   
1. 程序传送方式
	 * 程序查询方式分为无条件传送方式和查询方式（条件传送方式）两种。
	 	* 微机系统中的一些简单的外设，如开关、继电器、数码管、发光二极管等，在它们工作时，可以认为输入设备已随时准备好向CPU提供数据，而输出设备也随时准备好接收CPU送来的数据，这样，在CPU需要同外设交换信息时，就能够用IN或OUT指令直接对这些外设进行输入/输出操作。由于在这种方式下CPU对外设进行输入/输出操作时无需考虑外设的状态，故称之为无条件传送方式。 
  
	    * 查询传送也称为条件传送，是指在执行输入指令（IN）或输出指令（OUT）前，要先查询相应设备的状态，当输入设备处于准备好状态、输出设备处于空闲状态时，CPU才执行输入/输出指令与外设交换信息。为此，接口电路中既要有数据端口，还要有状态端口。  
	      
	      1．CPU从接口中读取状态字；  
   		  2．CPU检测相应的状态位是否满足“就绪”条件；  
          3．如果不满足，则重复1、2步；若外设已处于“就绪”状态，则传送数据。 

2. 中断传送方式

    * 中断传送方式是指当外设需要与CPU进行信息交换时，由外设向CPU发出请求信号，使CPU暂停正在执行的程序，转去执行数据的输入/输出操作，数据传送结束后，CPU再继续执行被暂停的程序。   
    
3. 直接存储器存取（DMA）
 	*  DMA传送方式是在存储器和外设之间、存储器和存储器之间直接进行数据传送(如磁盘与内存间交换数据、高速数据采集、内存和内存间的高速数据块传送等)，传送过程无需CPU介入，这样，在传送时就不必进行保护现场等一系列额外操作，传输速度基本取决于存储器和外设的速度。DMA传送方式需要一个专用接口芯片DMA控制器（DMAC）对传送过程加以控制和管理。进行DMA传送期间，CPU放弃总线控制权，将系统总线交由DMAC控制，由DMAC发出地址及读/写信号来实现高速数据传输。传送结束后DMAC再将总线控制权交还给CPU。
 	
### map reduce  

![](http://www.opensourceforu.com/wp-content/uploads/2011/03/MapReduce.jpg)
###数据库
1. 事务的属性包括四大类 ACID `atomic 原子性` `consistency 一致性` `isolation 隔离性` `durability 持久性`
2. 查询 student 表 第5到10条数据 select * from student limit 5,10


MYSQL 操作 出处：[http://jilili.blog.51cto.com/6617089/1190014](http://jilili.blog.51cto.com/6617089/1190014)  
3、修改表
ALTER TABLE tb_name;       
mysql>alter table students change course Course varchar(100) after name;    
mysql>alter table students add course varchar(100);       
向表中插入数据  
```
insert into tb_name （col，col2，....) values (val1,val2,....）;      
insert into tutors （Tname，Gender，Age） values ('jerry','M',24);  -----批量插入方式
insert into tutors set Tname='Tom',Genser='F',Age=30;            -----只能实现单个字段
```   
插入  

```
insert into tutors （Tname,Gender,Age) select Name,Genser,Age from students where Age >=20  
select * from tutors order by TID desc limit 1;          -----查看降序的第一行  
select last_insert_ID（）;      -----查询插入的最后一个序列号 
```   
更改数据库  

```
UPDATE tb_name SET column=value where   
mysql>update students set Course='wg' where Name='j'; ' -----更改j的课程为wg   
````
删除表中的某一字段  

`DELETE FROM students  WHERE Course=''; `  


6、select语句练习   
```
select distict Gender from students;         ------相同的内容只显示一次    
 
查找年龄大于20的同学并且按降序排列:   
select Name,Age from students where Age>20 order by Age desc;    
年龄大于等于20并且是男性的同学:     
select Name from students where Age>20 and Gender='M';  
年龄不大于20的同学:  
select Name,Age,Gender from students where not Age>20;    
小于等于20的女同学:  
select Name,Age,Gender from students where not （Age>20 or Gender=‘M’）;  
年龄在（21-24）之间的同学(以下两种方式）：  
select Name，Age from students where Age>20 and Age<25;  
select Name，Age from students where Age between 20 and 25;   
显示以Y开头的名称（这里限定了姓名的长度）("_"表示任意单个字符):   
select Name from students where Name like 'Y___';  
显示以Y开头的姓名：   
`select Name from students where Name like 'Y%';  `    
名称中含有ing的名称（“%”表示任意长度的任意字符):    
`select Name from students where Name like '%ing%';  `     
显示以M或N或Y开头的名字（支持正则表达式）:  
`select Name from students where Name rlike '^[MNY].*$'; `    
显示年龄是18、20、25的同学：  
`select Name from students where Age IN （18,20,25）; `     
显示挑选课程号(CID1)为空的同学：   
`select Name from students where CID1 is null; `   
把查询后的结果进行降序排序（ASC升序，desc降序）   
`select Name,CID1 from students where CID1 is not null order by CID1 desc;  ` 
显示查询的Name表头名变为name    
`select Name AS Student_Name from students;  `   
隔两行数据向后取三行数据：  
`select Name from students limit 2,3;  ` 
所有同学的平均年龄:  
`select AVG（age） from students;  `  
显示年龄最大的同学：  
select MAX（age） from students;   
显示年龄最小的同学：   
`select MIN（age） from students;  `  
显示所有同学的年龄总和：   
`select SUM（age） from students;  `  
显示所有同学的个数：    
`select count（age） from students; `   
显示所有男同学的平均年龄：  
`select AVG（age） from students where Gender=’M‘;`    
显示所有女同学的平均年龄：   
`select AVG（age） from students where Gender=’F‘; `  
显示男女同学的平均年龄：  
`select Gender,avg(age) from students group by Gender; `  
显示选修CID1的同学   
``select count(CID1) AS  Persons,CID1 from students group by CID1;`  
显示选修人数大于2的课程：   
``select count(CID1) AS  Persons,CID1 from students group by CID1 having Persons>=2;``
 
**多表查询**   
每位同学及其他所学习的课程名称（以下四种方式）  
``` 
select students.Name,courses.Cname from students，courses where   students.CID1=courses.CID;  
select s.Name,c.Cname from students AS s,courses AS c where s.CID1=c.CID;   
select s.Name,c.Cname from students AS s left jion courses AS c on s.CID1=c.CID;(左连接）
select s.Name,c.Cname from students AS s right jion courses AS c on s.CID1=c.CID;（右连接)
```  
显示各个同学与他相对应的导师：   
`select c.Name as student,s.Name as teacher from students as s,students as c where
 s.SID=c.TID;  ` 
显示每一位老师及其所教授的课程；没有教授的课程保持为NULL:    
`select t.Tname,c.Cname from tutors as t left join courses as c on t.TID=c.TID; `
显示每一个课程及其相关的老师，没有老师教授的课程将其老师显示为空:   
`select t.Tname,c.Cname from tutors as t right jion courses as c on t.TID=c.TID; `
显示每位同学CID1课程的课程名及其讲授了相关课程的老师的名称：  
```sql 
select Name,Cname,Tname from students,courses,tutors where students.CID1=courses.CID  
and courses.TID=tutors.TID; 
```  
查看同学的成绩及姓名，并且按升序排列：  
``` sql
select students.Name,scores.Score from students,scores where students.SID=scores.SID  
order by scores.Score desc; 
```
 
**子查询**   
挑选出courses表中没有被students中的CID2学习的课程的课程名称：  
`select Cname from courses where CID not IN (select CID2 from students where  
CID2 is not null); `
挑选出没有教授任何课程的老师，每个老师及其所教授课程的对应关系在courses表中：   
`select Tname from tutors where TID not in (select distinct TID from courses); `
找出students表中CID1有两个或两个以上同学学习了的同一个门课程的课程名称：   
`select Cname from courses where CID in (select CID1 from students group by CID1 
 having count(CID1) >=2); `
年龄大于平均年龄的同学：(使用子查询时，子查询只能返回单个值）：  
`select Name,Age from students where Age > (select avg(age) from students);  `
查询学生和老师各自的年龄并写在一个表中：   
`(select Name，Age from students) union (select Tname，Age from tutors); `


###进程

进程通信  
windows的进程间的通信方式有:  
1.文件映射；2. 共享内存（是文件映射的一种特殊情况）；3.邮件槽（mailslot）（点对点消息队列）; 4.匿名管道；5；命名管道； 6. 剪贴板；7.动态数据交换；8.对象链接与嵌入；9.远程过程调用；10.动态链接库；11.socket；12.WM_COPYDATA .  
linux进程间通信的方式有：1.管道 2.信号量 3.共享内存 4.消息队列 5.套接字 6.信号  
windows和linux共有的进程间通信方式：1. 消息（linux中叫做信号） 2. 共享内存  3. 邮槽  4. 管道   5.socket


