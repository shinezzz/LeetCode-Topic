# LeetCode 专题 -- 动态规划习题

## AcWing 285. 没有上司的舞会

`难度：简单`

### 题目描述

Ural大学有N名职员，编号为1~N。

他们的关系就像一棵以校长为根的树，父节点就是子节点的直接上司。

每个职员有一个快乐指数，用整数 Hi 给出，其中 1≤i≤N。

现在要召开一场周年庆宴会，不过，没有职员愿意和直接上司一起参会。

在满足这个条件的前提下，主办方希望邀请一部分职员参会，使得所有参会职员的快乐指数总和最大，求这个最大值。

**输入格式**:

第一行一个整数N。

接下来N行，第 i 行表示 i 号职员的快乐指数Hi。

接下来N-1行，每行输入一对整数L, K,表示K是L的直接上司。

**输出格式**:

输出最大的快乐指数。

**数据范围**:

- 1≤N≤6000,
- −128≤Hi≤127

```matlab
输入样例：
7
1
1
1
1
1
1
1
1 3
2 3
6 4
7 4
4 5
3 5
输出样例：
5
```

**链接**：https://www.acwing.com/problem/content/287/

### Solution

1. 动态规划

- **状态表示**：
  - dp[i][0] 表示不选第i个节点的收益
  - dp[i][1] 表示选择第i个节点的收益
  - 属性值：Max
- **状态计算**: (j为i的子节点)
  - 选择第i个节点：dp[i][1] += dp[j][0]
    - 不选第i个节点：dp[i][0] += Math.max(dp[j][0], dp[j][1]) 
- **初始化**:
  - dp[i][0] = 0;
  - dp[i][1] = w[i];

这道题和[LeetCode 337 打家劫舍 III](./337打家劫舍III.md)的思路是一样的。

这道题在Acwing上面，难点是自己利用**用数组模拟邻接表重建出一棵树**。我尝试在注释中备注了一下思路。

```java
import java.util.*;

class Main{
    final int N = 6010;
    final int INF = 0x3f3f3f3f;


    int[] w = new int[N]; // 存储快乐指数，每条边的收益
    // 建立邻接表存储树
    int[] head = new int[N];    // 存储邻接表的表头
    int[] edge = new int[N];    // 按输入顺序存储每条边指向的节点
    int[] next = new int[N];    // 记录邻接表中当前节点的下一个节点
    int idx = 1;                // 记录边的序号,边的序号从1开始吧

    boolean[] flag = new boolean[N];    // 记录第i个节点是否有父亲

    int[][] dp= new int [N][2];               // dp数组

    // 状态表示
    // dp[i][0] 表示不选第i个节点的收益
    // dp[i][1] 表示选择第i个节点的收益
    // 属性值：Max
    // 状态计算: (j为i的子节点)
    // 选择第i个节点：dp[i][1] += dp[j][0]
    // 不选第i个节点：dp[i][0] += Math.max(dp[j][0], dp[j][1]) 
    // 初始化
    // dp[i][0] = 0;
    // dp[i][1] = w[i];

    public void add(int a, int b){
        // 第idx边指向b 
        edge[idx] = b;
        // 采用头插法
        // 第idx边的下一个节点是上一个时刻的头节点
        next[idx] = head[a];
        // 当前链表头节点更新，指向第idx边
        head[a] = idx;
        // idx++ 更新边序号
        idx++;
    }
    public void dfs(int r){
        // 遍历当前节点的每一个子树
        // 深度优先
        dp[r][1] = w[r];
        for(int i = head[r]; i != 0; i = next[i]){

            int j = edge[i];
            dfs(j);
            dp[r][0] += Math.max(dp[j][0], dp[j][1]);
            dp[r][1] += dp[j][0];
        }

    }
    public void init(){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 1; i <= n; i++ ){
            w[i] = sc.nextInt();
        }
        for(int i = 1; i < n; i++){
            int son, fa;
            son = sc.nextInt();
            fa = sc.nextInt();
            add(fa, son);
            flag[son] = true;
        }
    }
    public int solve(){
        // 找根节点是第几条边
        // 数据范围从1开始
        int root = 1;
        // 因为是连续的，所以从小到大遍历，只要找到没有父亲的节点，那它就是根节点
        while(flag[root]) root++;
        // 深度优先搜索
        dfs(root);
        return Math.max(dp[root][0], dp[root][1]);
    }
    public static void main(String[] args) {
        Main s = new Main();
        s.init();
        int res = s.solve();
        // 返回选或者不选的根节点情况下的收益较大的一个。
        System.out.println(res);

    }
}
```
