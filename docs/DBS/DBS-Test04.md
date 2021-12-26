# 数据库原理及应用 习题四答案作者：陈九礼

*原文链接：[数据库原理及应用教程(第4版|微课版)陈志泊-第四章习题_陈九礼](https://blog.csdn.net/weixin_41640994/article/details/103781557)*

# 一、选择题
1. **B**
2.  **B**
3. **D**
4. **B**
5. **C**
6. **D**
7. **B**
8. **D**
9. **D**
10. **D**
11. **A**
12. **C**
13.  **D**
14. **C**
15. **B**
# 二、填空题
1. 超键（或超码）
2. 正确 、完备
3. 属性集X的闭包X<sup>+</sup> 、函数依赖集F的闭包F<sup>+</sup>
4. 平凡的函数依赖 、自反性
5. {AD→C} 、φ
6. 2NF 、3NF 、BCNF
7. 无损连接 、保持函数依赖
8. AB 、BC 、BD
9. B→φ 、B→B 、B→C 、B→BC
10.  B→C 、A→D 、D→C
11. AB 、1NF
12. AD 、2NF
13. BCNF
14. 包含
15. 函数依赖
16. BCNF
# 三、简答题

>  
 1．解释下列术语的含义：函数依赖、平凡函数依赖、非平凡函数依赖、部分函数依赖、完全函数依赖、传递函数依赖、范式、无损连接分解、保持函数依赖分解。 

<mark>函数依赖</mark>（Functional Dependency，FD）是关系模式中属性之间的一种逻辑依赖关系。当属性集Y是属性集X的子集（即Y X）时，则必然存在着函数依赖X→Y，这种类型的函数依赖称为<mark>平凡的函数依赖</mark>。如果Y不是X的子集，则称X→Y为<mark>非平凡的函数依赖</mark>；



设有关系模式R（U），U是属性全集，X和Y是U的子集，如果X→Y，并且对于X的任何一个真子集X′，都有X’ Y，则称Y对X<mark>完全函数依赖</mark>（Full Functional Dependency），记作X Y。如果对X的某个真子集X’，有X’→Y，则称Y对X<mark>部分函数依赖</mark>（Partial Functional Dependency），记作X→Y；



设有关系模式R（U），U是属性全集，X，Y，Z是U的子集，若X→Y，但Y X，而Y→Z（Y X，Z Y），则称Z对X<mark>传递函数依赖</mark>（Transitive Functional Dependency），记作：X →Z；



>  
 上面有些写不全，看下面图片的箭头 

关系模式规范化过程中为不同程度的规范化要求设立的不同标准称为<mark>范式</mark>



<mark>无损连接分解</mark>：设有关系模式R，F是R上的函数依赖集，R分解为数据库模式p = {R<sub>1</sub>, R<sub>2</sub>, . . . , R<sub>k</sub>}。如果对R中满足下的每一个关系r，有r = Π<sub>R1</sub>( r) ⋈ Π<sub>R2</sub>( r) ⋈ … ⋈ Π<sub>Rk</sub>( r)，那么久成分解p相对于F“无损连接分解”，简称“无损分解”，否则称为“损失分解”



<mark>保持函数依赖分解</mark>：设有关系模式R(U)，F是R(U)上的函数依赖集，Z是属性集U上的一个子集， p = {R<sub>1</sub>, R<sub>2</sub>, … R<sub>k</sub>}是R的一个分解 F在Z上的一个投影Π<sub>z</sub>(F)表示：Π<sub>z</sub>(F) = {X → Y | Y∈ F<sup>+</sup> ∧ XY ⊆ Z} F在R<sub>i</sub>上的一个投影用Π<sub>Ri</sub>(F)表示： <img src="https://img-blog.csdnimg.cn/20200105135914715.png" alt="在这里插入图片描述"> Π<sub>Ri</sub>(F) = Π<sub>R1</sub>(F) ∪ Π<sub>R2</sub>(F) ∪ … ∪ Π<sub>Rk</sub>(F) 如果有F<sup>+</sup> = （ <img src="https://img-blog.csdnimg.cn/20200105140249998.png" alt="在这里插入图片描述"> Π<sub>Ri</sub>(F) ）<sup>+</sup>



>  
 注意：上面的图片和下面的式子是连接在一起的 

<img src="https://img-blog.csdnimg.cn/20191231141950404.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY0MDk5NA==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">



>  
 2．给出2NF、3NF和BCNF的形式化定义，并说明它们之间的区别和联系 

如果关系模式R∈1NF，且每个非主属性都完全函数依赖于R的主码，则称R属于第二范式（Second Normal Form），简称2NF，记作R∈2NF;



如果关系模式R∈2NF，且每个非主属性都不传递函数依赖于R的主码，则称R属于第三范式（Third Normal Form），简称3NF，记作R∈3NF;



如果关系模式R∈1NF，且所有的函数依赖X→Y（Y X），决定因素X都包含了R的一个候选码，则称R属于BC范式（Boyce-Codd Normal Form），记作R∈BCNF;



区别和联系： 1）BCNF⊂3NF⊂2NF 2）BCNF、3NF与2NF均是针对函数依赖而定义划分的。2NF、3NF和BCNF是在函数依赖的条件下对模式分解所能达到的分离程度的测度。一个模式中的关系模式如果都属于BCNF，那么在函数依赖范畴内，它已实现了彻底的分离，已消除了插入和删除异常。



>  
 3.什么叫关系模式分解？为什么要有关系模式分解？模式分解要遵守什么准则？ 

设有关系模式R（U），R<sub>1</sub>，R<sub>2</sub>，…，R<sub>k</sub>都是R的子集（此处把关系模式看成是属性的集合），R=R<sub>1</sub>∪R<sub>2</sub>∪…∪R<sub>k</sub>，关系模式的集合用ρ表示，ρ={R<sub>1</sub>，R<sub>2</sub>，…，R<sub>k</sub>}。用ρ代替R的过程称为<mark>关系模式的分解</mark>



关系模式分解是为了消除关系模式中不合理的数据冗余和操作异常问题



衡量关系模式的一个分解是否可取，主要有两个标准： <mark>即分解是否具有无损连接</mark> <mark>分解是否保持了函数依赖</mark>



>  
 4.试证明全码的关系必是3NF，也必是BCNF 

设有关系R（U，F），因为R含全码，所以U中的属性均为主属性，即R不含任何非主属性; 根据3NF的定义，R中没有非主属性对码有传递函数依赖存在。根据定义可下结论：R∈3NF; 证毕。



>  
 5.设有关系模式R（A，B，C，D），函数依赖F={A→C，C→A，B→AC，D→AC，BD→A} 


1）求出R的所有候选码

```apl
候选码是BD

```

2）求出F的最小函数依赖集F<sub>min</sub>

```apl
{A→C，C→A，B→A，D→A}

```

3）根据函数依赖关系，确定关系模式R属于第几范式

```apl
第1范式

```

4）将R分解为3NF，并保持无损连接性和函数依赖性

```apl
P={AC，BA，DA，BD}

```

>  
 6.设有关系模式R（A，B，C，D），函数依赖F={A→C，C→A，B→AC，D→AC} 


1）求(AD)<sup>+</sup> ，B<sup>+</sup>

(AD)<sup>+</sup> =ACD，B<sup>+</sup>=ABC



2）求出R的所有候选码

```apl
BD

```

3）求出F的最小函数依赖集F<sub>min</sub>

```apl
{A→C，C→A，B→A，D→A}

```

4）根据函数依赖关系，确定关系模式R属于第几范式

```apl
第1范式

```

5）将R分解为3NF，并保持无损连接性和函数依赖性

```apl
P={R1(A，C)，R2(B，A)，R3(D，A)，R4(B，D)}

```

6）将R分解为BCNF，并保持无损连接性

```apl
P={R1(A，C)，R2(A，B，D) }

```

>  
 7.关系模式R（A，B，C，D，E），函数依赖F={A→D，E→D，D→B，BC→D，CD→A} 


1）求R的候选码

```apl
CE

```

2）根据函数依赖关系，确定关系模式R属于第几范式

```apl
第1范式

```

3）将R分解为3NF，并保持无损连接性

```apl
P={R1(A，C)，R2(B，C)，R3(C，D)，R4(D，E，C)，R5(C，E，A)，R6(B，E)}

```

>  
 8．判断以下关系模式的分解是否具有无损连接性 


1）关系模式R（U，V，W，X，Y，Z），函数依赖F={U→V，W→Z，Y→U，WY→X}，分解ρ={WZ，VY，WXY，UV}

```apl
否

```

2）关系模式R（B，O，I，S，Q，D），函数依赖F={S→D，I→B，IS→Q，B→O}，分解ρ={SD，IB，ISQ，BO}

```apl
是

```

3）关系模式R（A，B，C，D），函数依赖F={A→C，D→C，BD→A}，分解ρ={AB，ACD，BCD}

```apl
否

```

4）关系模式R（A，B，C，D，E），函数依赖F={A→C，C→D，B→C，DE→C，CE→A}，分解ρ={AD，AB，BC，CDE，AE}

```apl
否

```

>  
 9.设有关系模式SC(S，C，G），函数依赖集为F={SC→G}。请确定SC的范式等级，并证明 

候选码SC， 非主属性G都完全依赖于主码，属于第二范式； 非主属性G不传递函数依赖于主码，属于第三范式； 函数依赖决定因素包括候选码，属于BC范式； 对于函数依赖SC→G，SC包含了关系的候选码，属于第四范式



>   10．设有关系模式R（A，B，C，D，E，F），函数依赖集F={A→BC，BC→A，BC，D→EF，E→C}。试问：关系模式R是否为BCNF，并证明结论 

**无答案**




>   11．设有关系模式R（A，B，C，D，E），函数依赖集F={A→D，E→D，D→B，(B，C)→D，(D，C)→A} 

1）求出R的候选码

```apl
CE

```

2）判断ρ={AB，AE，CE，BCD，AC}是否为无损连接分解？

```apl
是

```

>  
 12．设有关系模式R（A，B，C，D，E），函数依赖集F={A→C，B→D，C→D，DE→C，CE→A}。判断ρ={AD，AB，BE，CDE，AE}是否为无损连接分解？ 


```apl
无损连接分解

```

>  
 13．设有函数依赖集F={AB→CE，A→C，GP→B，EP→A，CDE→P，HB→P，D→HG，ABC→PG}，求属性集D关于F的闭包D<sup>+</sup> 

<font color=#f6613b>D<sup>+</sup>={DGH}</font>




>  
 14．已知关系模式R的全部属性集U={A，B，C，D，E，G}及其函数依赖集：F={AB→C，C→A，BC→D，ACD→B，D→EG，BE→C，CG→BD，CE→AG}，求属性集BD的闭包(BD)<sup>+</sup> 



<font color=#f6613b>（BD)<sup>+</sup>={ABCDEG}</font>


>  
 15．设有函数依赖集F={D→G，C→A，CD→E，A→B}，求闭包D<sup>+</sup>、C<sup>+</sup>、A <sup>+</sup>、(CD)<sup>+</sup>、(AD)<sup>+</sup>、(AC)<sup>+</sup>、(ACD)<sup>+</sup> 

<font color=#f6613b>D<sup>+</sup>= {DG} C<sup>+</sup>= {ABC} (CD)<sup>+</sup>= {ABCDEG} (AD)<sup>+</sup>= {ABDG} (AC)<sup>+</sup>= {ABC} (ACD)<sup>+</sup>= {ABCDEG}</font>

>  
 16．设有函数依赖集F={AB→CE，A→C，GP→B，EP→A，CDE→P，HB→P，D→HG，ABC→PG}，求与F等价的最小函数依赖集 

<font color=#f6613b>F<sub>min</sub>={AB→E，A→C，GP→B，EP→A，CDE→P，HB→P，D→H，D→G，AB→P，AB→G}</font>

>  
 17．设有关系模式R（U，F），其中：U={E，F，G，H}，F={E→G，G→E，F→EG，H→EG，FH→E}，求F的最小函数依赖集 

<font color=#f6613b>F<sub>min</sub> = { E→G，G→E，F→E，H→E }</font>

>  
 18．求以下给定关系模式的所有候选码 


1）关系模式R（A，B，C，D，E，P），其函数依赖集F={A→B，C→P，E→A，CE→D}

```apl
CE

```

2）关系模式R（C，T，S，N，G），其函数依赖集F={C→T，CS→G，S→N}

```apl
CS

```

3）关系模式R（C，S，Z），其函数依赖集F={(C，S)→Z，Z→C}

```apl
CS，ZS

```

4）关系模式R（S，D，I，B，O，Q），其函数依赖集F={S→D，I→B，B→O，O→Q，Q→I}

```apl
SI，SB，SO，SQ

```

5）关系模式R（S，D，I，B，O，Q），其函数依赖集F={I→B，B→O，I→Q，S→D}

```apl
SI

```

6）关系模式R（A，B，C，D，E，F），其函数依赖集F={AB→E，AC→F，AD→B，B→C，C→D}

```apl
AB，AC，AD

```

>  
 19．设有关系R，如图4-36所示 试问R属于第几范式？如何规范化为3NF？写出规范化的步骤 


<img src="https://img-blog.csdnimg.cn/20200105144620317.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTY0MDk5NA==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

```apl
关系R主码为职工号，每个非主属性都完全函数依赖于主码，因此R属于第二范式。
因为单位名依赖于单位号，单位号依赖于职工号，即非主属性传递函数依赖于R的主码，
所以R不属于第三范式

```

规范化步骤：

1）求出关系模式R的最小函数依赖集

F<sub>min</sub>={职工号→职工名，职工号→年龄，职工号→性别，职工号→单位号，单位号→单位名}



2）根据算法4.6的第（2）步，可看出F中没有满足条件的函数依赖



3）根据算法4.6的第（3）步，将R分解为：R1={职工号，职工名，年龄，性别，单位号}，R2={单位号，单位名}



4）ρ={ R1={职工号，职工名，年龄，性别，单位号}，R2={单位号，单位名}}



>  
 20．要建立关于系、学生、班级、研究会等信息的一个关系数据库。规定：一个系有若干专业，每个专业每年只招一个班，每个班有若干学生，一个系的学生住在同一个宿舍区。每个学生可参加若干研究会，每个研究会有若干学生 


```apl
描述学生的属性有：学号、姓名、出生年月、系名、班号、宿舍区

描述班级的属性有：班号、专业名、系名、人数、入校年份

描述系的属性有：系号、系名、系办公室地点、人数

描述研究会的属性有：研究会名、成立年份、地点、人数
学生参加某研究会，有一个入会年份

```

试给出上述数据库的关系模式；写出每个关系的最小依赖集（基本的函数依赖集，不是导出的函数依赖）；指出是否存在传递函数依赖；对于函数依赖左部是多属性的情况，讨论其函数依赖是完全函数依赖还是部分函数依赖，指出各关系的候选码

##### 1）关系模式为：

系（{系号，系名，系办公室地点，宿舍区，人数}，{系号→系名，系号→系办公室地点，系名→系办公室地点，系号→宿舍区}）



班级（{班号，专业名，系号，人数，入校年份}，{班号→专业名，班号→系号，班号→入校年份，（专业名，入校年份）→班号}），其中，人数为冗余属性，可以通过计算指定班级号的人数获得



学生（{学号，姓名，出生年月，系号，班号}，{学号→姓名，学号→出生年月，学号→系号，学号→班号，学号→宿舍区，班号→系号}）



入会（{学号，研究会名，入会年份}，{（学号，研究会名）→入会年份}） 研究会（{研究会名，成立年份，地点，人数}，{研究会名→成立年份，研究会名→地点}），其中，人数为冗余属性，可以通过入会关系计算查询



##### 2）传递函数依赖有：系号→系办公室地点；学号→宿舍区



##### 3）以上关系模式中没有部分函数依赖

系关系中候选码为：系号；外码为：无

班级关系中候选键为：班号、（专业名，入校年份）；外码为：系号

学生关系中候选键为：学号；外码为：班号

入会关系中候选键为：（学号，研究会名）；外码为：学号或研究会名

研究会关系中候选键为：研究会名；外码为：无



>  
 21．设有函数依赖集F={AB→CE，A→C，GP→B，EP→A，CDE→P，HB→P，D→HG，ABC→PG}，求与F等价的最小函数依赖集 

<font color=#f6613b>F<sub>min</sub>={AB→E，A→C，GP→B，EP→A，CDE→P，HB→P，D→H，D→G，AB→P，AB→G}</font>

>  
 22．设有关系模式R(B，O，I，S，Q，D)，其上函数依赖集为：F={S→D，I→B，IS→Q，B→O}，如果用SD、IB、ISQ和BO代替R，这样的分解具有无损连接吗？ 

<font color=#f6613b>该分解是无损连接</font>

>  
 23．设关系R（课程名，教师名，教师地址），它是第几范式？是否存在删除异常？如何将它分解为高一级的范式 

<font color=#f6613b>关系R是第一范式。该关系的主码为（课程名，教师名），因为教师地址函数依赖于教师名，因此不满足每个非主属性都完全函数依赖于R的主码，因此不属于第二范式; 该关系存在删除异常，当某课程被删除时，相应的教师名和教师地址也被删除，但现实中该教师仍在存在; 关系R可分解为R1={课程名，教师名}，R2={教师名，教师地址}。</font>

