# LeetCode 专题 -- 搜索_DFS_BFS_回溯

## 52. N皇后 II

`难度：困难`

### 题目描述

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。
给定一个整数 n，返回 n 皇后不同的解决方案的数量。

```r
示例:

输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```

**提示**：

> - 皇后，是国际象棋中的棋子，意味着国王的妻子。皇后只做一件事，那就是“吃子”。当她遇见可以吃的棋子时，就迅速冲上去吃掉棋子。当然，她横、竖、斜都可走一或 N-1 步，可进可退。（引用自 百度百科 - 皇后 ）

**链接**：https://leetcode-cn.com/problems/n-queens-ii

### Solution

回溯的DFS模板

```java
List<> res = new LinkedList<>();
Deque<Integer> path =  new ArrayDeque<>();

void dfs(路径, 选择列表){
    if 满足结束条件{
        res.add(路径);
        return;
    }

    for 选择 in 选择列表{
        // 做选择;
        // 标记一下已经选了，有些题目不需要标记
        nums[i] = true;
        // 把选择的放进路径
        path.push(i)
        dfs(路径, 选择列表);
        
        // 恢复现场;
        path.pop();
        nums[i] = false;
    }
}
```

有一个**性质**是，主对角线差为常数，次对角线和为常数。

利用这个性质给斜线上做标记。

```java
class Solution {
    boolean[] cols, diag, sub;
    int res;
    public int totalNQueens(int n) {
        // 用来做标记，列，主对角线，副对角线
        // 主对角线行列相减为常数
        // 副对焦先行列相加为常数
        cols = new boolean[n];
        diag = new boolean[2 * n];
        sub = new boolean[2 * n];

        // 递归行，从第0行开始
        dfs(0,n);
        return res;
    }
    void dfs(int row, int n){
        if(row == n){
            res++;
            return;
        }

        // 每一行从第0列开始递归
        for(int i = 0; i < n; i++){
            // 保证行，列，主对角线，副对角线
            if(!(cols[i] || diag[row - i + n] || sub[row + i]) ){
                cols[i] = diag[row - i + n] = sub[row + i] = true;
                dfs(row + 1, n);
                cols[i] = diag[row - i + n] = sub[row + i] = false;
            }
        }
    }
}
```