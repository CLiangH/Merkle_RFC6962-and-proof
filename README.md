实验目标
=

Impl Merkle Tree following RFC6962

• Construct a Merkle tree with 10w leaf nodes

• Build inclusion proof for specified element

• Build exclusion proof for specified element

实验流程
=

__前期准备__
______________

此实验我们使用一维数组代表merkle树，数组元素为我们的自写结构体，其中包含左右子树以及父节点的引用标号、Hash值、节点深度等变量。

此处的Hash函数我们使用C++11自带的函数，在此只做示范使用。

__Merkle函数__
______________

我们依次按照此种顺序将Hash值写入对应数组元素，并设置其高度（根据每次轮回不同，节点高度应对应增加）、子树节点以及父节点等。

![image](https://github.com/CLiangH/Picture/blob/main/M1.png)

倘若该层节点不足以两两分完，则将最后一个节点记录下来，并以它为头节点对应的树上的所有节点高度均加一，作为下一层节点进行，此处是为了符合RFC6962要求。

待所有节点均被设置，Merkle树创建完毕。

__Merkle_proof函数__
_________________

遍历证明节点的审查路径，观察是否可以得出根节点Hash值，以此进行存在性证明。

一个审查路径实例如下

![image](https://github.com/CLiangH/Picture/blob/main/M2.png)

__Merkle_not_proof函数__
_________________

证明目标数值左右两个值均在Merkle树中，且两值相邻，即可证明目标数值不在Merkle树中（此处为了方便，原始数值均按顺序排列）。

__项目测试__
_________________

我们创建具有100000个叶子节点的Merkle树，并证明4在这个树中，5.5不在这个树中。

后经测试发现，试验成功。

![image](https://github.com/CLiangH/Picture/blob/main/M3.png)
