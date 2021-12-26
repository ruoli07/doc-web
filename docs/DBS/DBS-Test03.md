# 数据库原理及应用 习题三 答案作者：陈九礼

*原文链接：[数据库原理及应用教程(第4版|微课版)陈志泊-第三章习题_陈九礼](https://blog.csdn.net/weixin_41640994/article/details/103685701)*

# 一、选择题
1. **B**
2. **A**
3. **C**
4. **B**
5. **C**
6. **C**
7. **B**
8. **D**
9. **A**
10. **D**
11. **D**
---------------------------------------------
# 二、填空题
1. 结构化查询语言（Structured Query Language）
2. 数据查询、数据定义、数据操纵、数据控制
3. 外模式、模式、内模式
4. 数据库、事务日志
5. NOT NULL约束、UNIQUE约束、PRIMARY KEY约束、FOREIGN KEY约束、CHECK约束
6. 聚集索引、非聚集索引
7. 连接字段
8. 行数
9. 定义
10. 系统权限、对象权限
11. 基本表、视图
12. 
```sql
1）INSERT INTO S VALUES('990010','李国栋','男',19)
2）INSERT INTO S(No,Name) VALUES('990011', '王大友')
3）UPDATE S SET Name='陈平' WHERE No='990009'
4）DELETE FROM S WHERE No='990008'
5）DELETE FROM S WHERE Name LIKE '陈%'
```



13. CHAR(8) NOT NULL
14. SC.CNo=C.CNo
15. ALTER TABLE Student ADD SGrade CHAR(10)

----------------------------------------------

# 三、设计题

1、设有以下两个数据表，各表中的结果及字段名如下： 图书（Book）包括书号（BNo）、类型（BType）、书名（BName）、作者（BAuth）、单价（BPrice）、出版社号（PNo）；

出版社（Publish）包括出版社号（PNo）、出版社名称（PName）、所在城市（PCity）、电话（PTel）；

用SQL实现下述功能： 1）在“高等教育出版社”出版、书名为“操作系统”的图书的作者名；

```sql
SELECT BAuth 
FROM Book,Pubish 
WHERE Book.PNo=Publish.PNo 
AND BName=’操作系统’ AND PName=’高等教育出版社’

```

2）查找为作者“张欣”出版全部“小说”类图书的出版社的电话；

```sql
SELECT PTel 
FROM Book,Pubish 
WHERE Book.PNo=Pubish.PNo 
AND BType=’小说’ AND BAuth=’张欣’

```

3）查询“电子工业出版社”出版的“计算机”类图书的价格，同时输出出版社名称及图书类别；

```sql
SELECT BPrice,PName,Btype 
FROM Book,Pulish 
WHERE Book.PNo=Pubish.PNo 
AND PName=’电子工业出版社’ AND BType=’计算机’

```

4）查找比“人民邮电出版社”出版的“高等数学”价格低的同名书的有关信息；

```sql
SELECT * 
FROM Book 
WHERE BName=’高等数学’ 
AND BPrice&lt; ANY(SELECT BPrice FROM Book,Pubish WHERE Book.PNo=Pubish.PNo 	AND PName=’人民邮电出版社’ AND BName=’高等数学’) 
AND PName&lt;&gt;’人民邮电出版社’

```

5）查找书名中有“计算机”一词的图书的书名及作者；

```sql
SELECT BName,BAuth FROM Book WHERE BName LIKE ‘%计算机%’

```

6）在“图书”表中增加“出版时间”（BDate）项，其数据类型为日期型；

```sql
ALTER TABLE Book ADD BDate datetime

```

7）在“图书”表中以“作者”建立一个索引。

```sql
CREATE INDEX Name ON Book (BAuth)

```

2、假设有一个书店，书店的管理者要对书店的经营状况进行管理，需要建立一个数据库，其中包括两个表： 存书（书号，书名，出版社，版次，出版日期，作者，书价，进价，数量） 销售（日期，书号，数量，金额）

请用SQL实现书店管理者的下列要求： 1）建立存书表和销售表；

```sql
CREATE TABLE Book(
	BNo CHAR(10) PRIMARY KEY,
	BName	VARCHAR(50) NOT NULL,
	Publish	VARCHAR(50),
	Version	FLOAT,
	PDate	DATE,
	BAuth	VARCHAR(30),
	BPirce	NUMERIC(4,1),
	BInPrice	NUMERIC(4,1),
	BCount	INT
);

CREATE TABLE BookSell(
	BSID CHAR(20) PRIMARY KEY,
	BNO	CHAR(8) CONSTRAINT B_C FOREIGN KEY REFERENCES Book(BNo),
	SDate	DATE,
	SCount	INT,
	PDate	DATETIME,
	SMoney	SMALLMONEY
);

```

2）掌握书的库存情况，列出当前库存的所有书名、数量、余额（余额=进价×数量，即库存占用的资金）；

```sql
SELECT BName,BCount,BInPrice*BCount AS TOTALCOUNT 
FROM Book

```

3）统计总销售额；

```sql
SELECT SUM(SCount*SMoney), SDate AS TOTALMONEY 
FROM BookSell 
GROUP BY SDate

```

4）列出每天的销售报表，包括书名、数量和合计金额（每一种书的销售总额）；

```sql
SELECT BNo,BName,SDate,BCount,SCount*SMoney AS TOTALMONEY
FROM BookS,BookSell 
WHERE Book.BNo=BookSell.BNo

```

5）分析畅销书，即列出本期（从当前日期起，向前30天）销售数量大于100的书名、数量。

```sql
SELECT BName,SCount
 FROM Book,BookSell 
 WHERE BookStore.BNo=BookSell.BNo 
 AND SCount&gt;100 AND SDate+30&lt;(SELECT MAX(SDate) FROM BookSell)

```

# 四、简答题

>  
 1、简述SQL支持的三级逻辑结构。 

SQL支持数据库的三级模式结构。外模式对应于视图和部分基本表，模式对应于基本表，内模式对应于存储文件；



>  
 2、SQL有什么特点？ 


SQL具有简单、易学、综合、一体等鲜明的特点，主要有以下几个方面: 1）SQL是类似于英语的自然语言，语法简单，且只有为数不多的几条命令，简洁易用;

2）SQL是一种一体化的语言，它包括数据定义、数据查询、数据操纵和数据控制等方面的功能，可以完成数据库活动中的全部工作;

3）SQL是一种非过程化的语言;

4）SQL是一种面向集合的语言，每个命令的操作对象是一个或多个关系，结果也是一个关系;

5）SQL既是自含式语言，又是嵌入式语言。自含式语言可以独立使用交互命令，适用于终端用户、应用程序员和DBA；嵌入式语言使其嵌入在高级语言中使用，供应用程序员开发应用程序。



>  
 3、解释本章所涉及的有关基本概念的定义：基本表、视图、索引、系统权限、对象权限、角色，并说明视图、索引、角色的作用 


<mark>基本表</mark>（Base Table）：一个关系对应一个基本表；

<mark>视图</mark>（View）：视图是从一个或几个基本表导出的表，是一个虚表；

<mark>索引</mark>是一种可以加快检索的数据库结构，它包含从表或视图的一列或多列生成的键，以及映射到指定数据存储位置的指针；

<mark>系统权限</mark>是指被授权用户是否可以连接到数据库上及数据库中可以进行哪些系统操作；

<mark>对象权限</mark>是指用户对数据库中具体对象所拥有的权限,对象权限针对某个特定的模式对象执行操作的权利,只能针对模式来设置和管理；

视图通常用来集中、简化和自定义每个用户对数据库的不同认识，可用作安全机制，可用于提供向后兼容接口来模拟曾经存在但其架构已更改的基础表，还可以在向SQL Server复制数据和从其中复制数据时使用视图，以便提高性能并对数据进行分区；

通过创建设计良好的索引，可以显著提高数据库查询和应用程序的性能。除提高检索速度外，索引还可以强制表中的行具有唯一性，从而确保数据的完整性；

<mark>角色</mark>用于区分不同的数据库用户，通过不同的权限设置，可保证数据在数据库中，为便于对用户及权限进行管理，可以将一组具有相同权限的用户组织在一起，这一组具有相同权限的用户就称为角色(Role)。使用角色能够更加方便和高效地对权限进行管理。



>  
 4、在对数据库进行操作的过程中，设置视图机制有什么优点？它与数据表有什么区别？ 


视图通常用来集中、简化和自定义每个用户对数据库的不同认识，可用作安全机制，可用于提供向后兼容接口来模拟曾经存在但其架构已更改的基础表，还可以在向SQL Server复制数据和从其中复制数据时使用视图，以便提高性能并对数据进行分区。

视图是一个虚拟表，其内容由查询定义，视图在数据库中并不是以数据值存储集形式存在，除非是索引视图。视图中的行和列数据来自定义视图的查询所引用的基本表，并且在引用视图时动态生成。



>  
 5、设有如下四个基本表S，C，SC，T，结构如图3-20所示 

<img src="https://img-blog.csdnimg.cn/20191224191907172.png" alt="在这里插入图片描述"> <img src="https://img-blog.csdnimg.cn/20191224191946937.png" alt="在这里插入图片描述"><img src="https://img-blog.csdnimg.cn/20191224191929594.png" alt="在这里插入图片描述"><img src="https://img-blog.csdnimg.cn/20191224192003390.png" alt="在这里插入图片描述">

图3-20 某教学数据库实例

 1）用SQL的DDL语言创建S表，S#为主码，SN不能为空；

```sqlite
CREATE TABLE S(
	S# CHAR(8) PRIMARY KEY,
	SN CHAR(8) NOT NULL,
	AGE INT,
	DEPT VARCHAR(20)
);

```

2）创建计算机系学生的视图，该视图的属性列由学号、姓名、课程号和任课教师号组成；

```sqlite
CREATE VIEW computer_student(S#,SN,C#,T#) AS 
SELECT S.S#,SN,SC.C#,T# FROM S,SC,T 
WHERE S.S#=SC.S# AND SC.C#=T.C# AND DEPT=’计算机’

```

3）检索计算机系年龄在20岁以上的学生学号；

```sqlite
SELECT S# FROM S WHERE AGE&gt;20 AND DEPT=‘计算机’

```

4）检索姓王的教师所讲课程的课程号及课程名称；

```sql
SELECT C.C#,CN FROM C,T WHERE C.C#=T.C# AND TN LIKE ‘王%’

```

5）检索张三同学所学课程的成绩，列出SN、C#和GR；

```sqlite
SELECT SN,C#,GR
FROM S,SC WHERE S.S#=SC.S# AND SN=‘张三’

```

6）检索选修总收入超过1000元的教师所讲课程的学生姓名、课程号和成绩；

```sql
SELECT SN,T.C#,GR FROM T,SC,S 
WHERE T.C#=SC.C# AND S.S#=SC.S# AND (SAL+COMM)&gt;1000

```

7）检索没有选修C1课程且选修课程数为两门的学生的姓名和平均成绩，并按平均成绩降序排列；

```sqlite
SELECT S.S#,SN,AVG(GR) AS AVGSCORE FROM S,SC 
WHERE S.S#=SC.S# AND C#&lt;&gt;’C1’ 
GROUP BY S.S#,SN HAVING COUNT(*)=2 ORDER BY AVG(GR) DESC

```

8）检索选修和张三同学所选课程中任意一门相同的学生姓名、课程名；

```sqlite
SELECT SN,CN FROM S,SC,C 
WHERE S.S#=SC.S# AND C.C#=SC.C# AND C# 
IN (SELECT C# FROM S,SC 
WHERE S.S#=SC.S# AND SN=‘张三’) AND SN&lt;&gt;’张三’

```

9）S1同学选修了C3，将此信息插入SC表中；

```sqlite
INSERT INTO SC(S#,C#) VALUES (‘S1’, ‘C3’)

```

10）删除S表中没有选修任何课程的学生记录；

```sqlite
DELETE FROM S WHERE S# NOT IN (SELECT DISTINCT S# FROM SC)

```
