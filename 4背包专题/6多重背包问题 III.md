# LeetCode 专题 -- 背包专题

## 6. 多重背包问题 III

`难度：太难了`

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

> - 0 < N ≤ 1000
> - 0 < V ≤ 20000
> - 0 < vi,wi,si ≤ 20000

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

**提示**:

本题考查多重背包的单调队列优化方法。

**进阶**：

> 一维dp数组

**链接**：
> <https://www.acwing.com/problem/content/6/>

### Solution


**普通版**：

```java

```

**进阶版**：

```java

```

yxc

```cpp
#include <cstring>
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 20010;

int n, m;
int f[N], g[N], q[N];

int main()
{
    cin >> n >> m;
    for (int i = 0; i < n; i ++ )
    {
        int v, w, s;
        cin >> v >> w >> s;
        memcpy(g, f, sizeof f);
        for (int j = 0; j < v; j ++ )
        {
            int hh = 0, tt = -1;
            for (int k = j; k <= m; k += v)
            {
                if (hh <= tt && q[hh] < k - s * v) hh ++ ;
                while (hh <= tt && g[q[tt]] - (q[tt] - j) / v * w <= g[k] - (k - j) / v * w) tt -- ;
                q[ ++ tt] = k;
                f[k] = g[q[hh]] + (k - q[hh]) / v * w;
            }
        }
    }

    cout << f[m] << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/117236/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
