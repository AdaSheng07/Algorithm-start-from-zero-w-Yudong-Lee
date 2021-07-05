## 树与图

### 树、二叉树、树的遍历、树的序列化

#### 树（Tree）


![image](https://user-images.githubusercontent.com/86143164/124374215-fe6d9b80-dccb-11eb-89f7-c925a1127f93.png)


**定义树的结点-代码**
```C++
// C++
struct TreeNode {
    int cal;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x)
        : val(x), left(nullptr}, right(nullptr) {}
```

```Java
// Java
public class TreeNode {
    public int val;
    public TreeNode left, right;
    public TreeNode(int val) {
        this.val = null;
        this.right = null;
    }
}
```

```Python
# Python
class TreeNode:
    def _init_(self, val):
        self.val = val
        self.left, self.right = None, None
```


#### 二叉树（Binary Tree）


**二叉树的遍历**

前序遍历（Pre-order）

中序遍历（In-order）

后序遍历（Post-order）

层次序

#### 树的遍历

前序遍历、中序遍历和后序遍历一般用**递归**来求，树的前序遍历又称树的**深度优先遍历**  
层次序一般借助**队列**来求，树的层序遍历又称树的**广度优先遍历**

![image](https://user-images.githubusercontent.com/86143164/124374415-96b85000-dccd-11eb-9f12-715e718aea59.png)

**广度优先遍历**


**深度优先遍历**


-------

[二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)


[N叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)


[N叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)


[二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)


[从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)


[**Homework**  从中序与后续遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

***从前序与后序遍历序列，并不能唯一确定一棵二叉树**


-------

### 树的直径、最近公共祖先、树的变形


树的直径

[最近公共祖先（LCA）](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

**基环树（pseudotree / unicyclic graph）**

向一棵树添加一条边，形成一个环  
N个结点N条边

![image](https://user-images.githubusercontent.com/86143164/124374745-80f85a00-dcd0-11eb-85b6-839be77623d3.png)


-------

### 图、图的遍历

#### 图

![image](https://user-images.githubusercontent.com/86143164/124423732-596cc480-dd98-11eb-81e8-d5bce7b23467.png)


**链表、树、图的关系**

链表是特殊化的树  
树是特殊化的图  
- N个点N-1条边的连通无向图——树（N-1为无环的最多边数）
- N个点N条边的连通无向图——基环树

**图的存储**

- 图的矩阵、数组与邻接表表示

![image](https://user-images.githubusercontent.com/86143164/124424830-465af400-dd9a-11eb-869b-6b0d2501f497.png)


- 在图中加一条边：将矩阵对应位置由0改1，出边数组对应更新，邻接表在表头插入（效率高，无需遍历全链表）新结点

![image](https://user-images.githubusercontent.com/86143164/124425725-8c648780-dd9b-11eb-99e7-8f3b54ff0022.png)


无向图如何存储？

将无向图看作正反两条边的有向图：

![image](https://user-images.githubusercontent.com/86143164/124426447-a2267c80-dd9c-11eb-8a40-4f862135a26a.png)

所以也可以将无向图称为**双向图**，所有的图都是有向图。

如果边有长度，将邻接矩阵内的数存为长度权值，数组中的元素更新为`[Node, Length]`的`List<List[Node, Int]>`，或`pair`，或`class`。

时间复杂度：邻接矩阵始终是`O(n^2)`，出边数组与邻接表是`O(n + m)`


**图的存储 代码实现**

![image](https://user-images.githubusercontent.com/86143164/124427545-1877ae80-dd9e-11eb-92e9-f46865fee6c6.png)

-------

#### 图的遍历

**深度优先遍历**

![image](https://user-images.githubusercontent.com/86143164/124428095-d26f1a80-dd9e-11eb-8eaa-3340bcce7f12.png)


[课程表](https://leetcode-cn.com/problems/course-schedule/)




**广度优先遍历**








