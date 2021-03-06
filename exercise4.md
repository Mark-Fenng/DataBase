姓名：冯运
学号：1160300524

1. 有两个函数依赖的集合 F 和 G：
   （a）F={A→C，AC→D，E→AD，E→H}
   （b）G={A→CD，E→AH}
   F 和 G 等价吗？说明理由。
   答：等价
   证明：
   先求 F 的极小函数依赖集,对于 AC->D,由于$D\in A_F^+$，所以可以由 A->D 替代该函数依赖
   E->AD 可由 E->A 替代，因为去掉 E->D,依然有$D\in E_G^+$
   所以 F 的最小函数依赖集为{A->C,A->D,E->A,E->H}
   再求 G 的极小函数依赖集，很容易求得 G 的最小函数依赖集为{A->C,A->D,E->A,E->H}
   即 F 和 G 的最小函数依赖集是相同的，所以 F 和 G 是等价的

2) 下列关系模式是第几范式？说明理由。

    （1）R(X,Y,Z), F={Y→Z,XZ→Y}
    是第三范式，从函数依赖集中可以判断出 XZ 是候选集，而且每一个非键属性都完全依赖于键属性，非键属性都不传递依赖于键属性，确定是第三范式，但是 Y->Z 不满足 Y 是候选键，所以不是 BC 范式

    （2）R(X,Y,Z), F={Y→Z,Y→X,X→YZ}
    是 BC 范式，因为候选键是 Y,X,而且 Z,X 完全依赖于 Y,YZ 完全依赖于 X,不存在传递依赖，满足 BC 范式的要求。

    （3）R(W,X,Y,Z), F={X→Z,WX→Y}
    是第一范式，因为在 F 中，WX 是候选键，而 Y 完全依赖于候选键，Z 部分依赖于候选键，所以不满足第二范式的要求。

3) 设有关系模式 R(E,F,G,H)，其上有函数依赖集：

    F={E→G,G→E,F→EG,H→EG,FH→E}

    求 F 的最小函数依赖集。

    ```
    首先按照规则一拆解得到：
    G={
        E->G,
        G->E,
        F->E,
        F->G,
        H->E,
        H->G,
        FH->E
    }
    按照规则二删去 F->E,F->G,H->E,H->G
    按照规则三，将FH->E拆解为 F->E,H->E
    所以，最终F的最小函数依赖集为：
    {
        E->G,
        G->E,
        F->E,
        H->E
    }
    ```

4) 设有关系模式 R(A,B,C,D,E)，R 的函数依赖集是：

    F={A→D,E→D,D→B,BC→D,CD→A}

    将 R 保持函数依赖地分解成 3NF。

    ```
    1.先求F的最小依赖集
    经过验证，F就是自己的最小依赖集
    2.然后根据3NF分解算法得到如下的关系
    R(A,D)
    R(E,D)
    R(B,D)
    R(B,C,D)
    R(A,C,D)
    ```

5.  设有关系模式 R{A,B,C,D,E}，其上有函数依赖集：

    F={A→C,C→D,B→C,DE→C,CE→A}

    （1）求所有候选键。

    （2）判断 ρ={AD,AB,BC,CDE,AE}是否是无损连接分解？

    （3）把 R 分解为 BCNF，并具有无损连接性。

    答：
    (1)B 和 E 是 L 类属性
    $(BE)^+=\{ ABCDE \}$
    所以{BE}是候选键，且是唯一候选键
    (2)
    初始化矩阵如下：
    |     | A   | B   | C   | D   | E   |
    | --- | --- | --- | --- | --- | --- |
    | AD  | a1  | b12 | b13 | a4  | b15 |
    | AB  | a1  | a2  | b23 | b24 | b25 |
    | BC  | b31 | a2  | a3  | b34 | b35 |
    | CDE | b41 | b41 | a3  | a4  | a5  |
    | AE  | a1  | b51 | b53 | b54 | a5  |

    A->C
    |     | A   | B   | C   | D   | E   |
    | --- | --- | --- | --- | --- | --- |
    | AD  | a1  | b12 | b13 | a4  | b15 |
    | AB  | a1  | a2  | b13 | b24 | b25 |
    | BC  | b31 | a2  | a3  | b34 | b35 |
    | CDE | b41 | b41 | a3  | a4  | a5  |
    | AE  | a1  | b51 | b13 | b54 | a5  |

    C->D
    |     | A   | B   | C   | D   | E   |
    | --- | --- | --- | --- | --- | --- |
    | AD  | a1  | b12 | b13 | a4  | b15 |
    | AB  | a1  | a2  | b13 | a4  | b25 |
    | BC  | b31 | a2  | a3  | a4  | b35 |
    | CDE | b41 | b41 | a3  | a4  | a5  |
    | AE  | a1  | b51 | b13 | a4  | a5  |

    B->C
    |     | A   | B   | C   | D   | E   |
    | --- | --- | --- | --- | --- | --- |
    | AD  | a1  | b12 | b13 | a4  | b15 |
    | AB  | a1  | a2  | a3  | a4  | b25 |
    | BC  | b31 | a2  | a3  | a4  | b35 |
    | CDE | b41 | b41 | a3  | a4  | a5  |
    | AE  | a1  | b51 | b13 | a4  | a5  |

    DE->C
    |     | A   | B   | C   | D   | E   |
    | --- | --- | --- | --- | --- | --- |
    | AD  | a1  | b12 | b13 | a4  | b15 |
    | AB  | a1  | a2  | a3  | a4  | b25 |
    | BC  | b31 | a2  | a3  | a4  | b35 |
    | CDE | b41 | b41 | a3  | a4  | a5  |
    | AE  | a1  | b51 | a3  | a4  | a5  |

    CE->A
    |     | A   | B   | C   | D   | E   |
    | --- | --- | --- | --- | --- | --- |
    | AD  | a1  | b12 | b13 | a4  | b15 |
    | AB  | a1  | a2  | a3  | a4  | b25 |
    | BC  | b31 | a2  | a3  | a4  | b35 |
    | CDE | a1  | b41 | a3  | a4  | a5  |
    | AE  | a1  | b51 | a3  | a4  | a5  |

    因为最后的矩阵中没有全a的行，所以不是无损连接

    (3)
    R{A,B,C,D,E}
    F={A→C,C→D,B→C,DE→C,CE→A}
    初始时，$\tau=\{R\}$
    1.A→C函数依赖不满足BCNF条件，将其分解成R(AC)、R(ABDE)
    剩余化简的函数依赖为{B→D,BE→A}
    2.B→D函数依赖不满足BCNF条件，BD和ABE
    剩余化简的函数依赖为{BE→A}。
    3.BE->A满足BCNF条件

    所以最终的分解结果为
    R(A,C),R(B,D),R(A,B,E)
    


6.  考虑关系R，R 有一所大学的课程和章节的信息。

    R={课程编号，章节编号，学院，课时，等级，教师编号，学期，年，上课时间，教室，学生数量}

    假设 R 上有以下函数依赖关系：

    （a）{课程编号} -> {学院, 课时, 等级}

    （b）{课程编号, 章节编号,学期, 年} -> {上课时间, 教室, 学生数量, 教师编号}

    （c）{教室, 上课时间, 学期, 年} -> {教师编号, 课程编号, 章节编号}

    （1）R 的主键是？
        R的主键是{课程编号，章节编号，学期，年}
    （2）怎么把这个关系模式规范化？试分析之。
        这个关系是1NF,可能存在插入删除异常，数据冗余和更新问题
        可以使用3NF分解算法或BCNF分算法将该关系分解，提高关系的范式，从而解决这些可能存在的问题。
        例如可以将R拆分成
        R(课程编号，学院，课时，等级)
        和R(课程编号，章节编号，学期，年，上课时间，教室，学生数量，教师编号)
        两个关系，这样这两个关系就都满足了BCNF
