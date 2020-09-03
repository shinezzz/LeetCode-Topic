# LeetCode 专题 -- 背包专题

## 5. 多重背包问题 II

`难度：中等`

### 题目描述

有 N 种物品和一个容量是 V 的背包。

第 i 种物品最多有 si 件，每件体积是 vi，价值是 wi。

求解将哪些物品装入背包，可使物品体积总和不超过背包容量，且价值总和最大。

输出最大价值。

**输入格式**

第一行两个整数，N，V，用空格隔开，分别表示物品种数和背包容积。

接下来有 N 行，每行三个整数 vi,wi,si，用空格隔开，分别表示第 i 种物品的体积、价值和数量。

**输出格式**
输出一个整数，表示最大价值。

**数据范围**：

0 < N ≤ 1000
0 < V ≤ 2000
0 < vi,wi,si ≤ 2000

```matlab
输入样例
4 5
1 2 3
2 4 1
3 4 3
4 5 2
输出样例：
10
```

**提示**：

本题考查多重背包的二进制优化方法。

**进阶**：

> 一维dp数组

**链接**：
> <https://www.acwing.com/problem/content/5/>

### Solution


数据范围为1000，所以`O(N*V*s)`的复杂度会超时。

因此通过二进制优化降低复杂度。

**二进制优化**：
比如$10 =2^0 + 2^1 + 2^2+3$

**普通版**：

```java
import java.util.*;

class Main{
    static class Pair{
        int v,w;

        public Pair(int v, int w) {
            this.v = v;
            this.w = w;
        }
    }
    public static void main(String[] args){
        List<Pair> list = new LinkedList<>();

        Scanner scan = new Scanner(System.in);
        int N = scan.nextInt();
        int V = scan.nextInt();

        for(int i = 1; i <= N; i++){
            int v = scan.nextInt();
            int w = scan.nextInt();
            int s = scan.nextInt();
            for(int k = 1; k < s; k *= 2){
                s -= k;
                list.add(new Pair(k * v, k * w));
            }
            list.add(new Pair(s * v, s * w));
        }
        N = list.size();
        int[][] dp = new int[N + 1][V + 1];
        for(int i = 1; i <= N; i++){
            Pair p = list.get(i - 1);
            for(int j = 1; j <= V; j++){
                dp[i][j] = dp[i - 1][j];
                if(j >= p.v)  dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - p.v] + p.w);
            }
        }
        System.out.println(dp[N][V]);
    }
}
```

**进阶版**：

```java
import java.util.*;

class Main{
    static class Pair{
        int v,w;

        public Pair(int v, int w) {
            this.v = v;
            this.w = w;
        }
    }
    public static void main(String[] args){
        List<Pair> list = new LinkedList<>();

        Scanner scan = new Scanner(System.in);
        int N = scan.nextInt();
        int V = scan.nextInt();

        for(int i = 1; i <= N; i++){
            int v = scan.nextInt();
            int w = scan.nextInt();
            int s = scan.nextInt();
            for(int k = 1; k < s; k *= 2){
                s -= k;
                list.add(new Pair(k * v, k * w));
            }
            list.add(new Pair(s * v, s * w));
        }
        N = list.size();
        int[] dp = new int[V + 1];
        for(Pair p : list){
            // Pair p = list.get(i - 1);
            for(int j = V; j >= p.v; j--){
                dp[j] = Math.max(dp[j], dp[j - p.v] + p.w);
            }
        }
        System.out.println(dp[V]);
    }
}
```
