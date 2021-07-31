# L11 - L13 图遍历

## DFS

|       |  TE  |  BE  |  DE  |  CE  |
| :---: | :--: | :--: | :--: | :--: |
| d-DFS |  ✔   |  ✔   |  ✔   |  ✔   |
| u-DFS |  ✔   |  ✔   |  ×   |  ×   |
| d-BFS |  ✔   |  ✔   |  ×   |  ✔   |
| u-BFS |  ✔   |  ×   |  ×   |  ✔   |

u --> v：TE: white；BE：grey；DE,CE：black

### 有向图

topo --> 关键路径：利用DFS 尽头节点的性质。

```c
dfs(v){
		v.color = GRAY;
		for (auto& w: graph[v])
        if(w.color == WHITE)
            dfs(w);
    v.color = BLACK;
    topo.push(v);
}
```

SCC：第一次dfs，节点遍历结束入栈（->black)，【总的来看栈中存储了一个一个强连通片，首节点是最后一个入栈的】，把图转置，出栈遍历一遍

### 无向图

割点（某一个没有BE)，桥（全部没有BE)k

```c++
v.color = GRAY;
time++;
v.discovertime=v.back=time;//back larger
for (auto& w: graph[v]){
    if(w.color == WHITE){
	    		dfs(w);
        if(w.back >= v.discovertime)
            output v as cut-point;
        v.back=min(v.back,w.back)
        if(w.back > v.discovertime)
            output v as bridge;
    }
    else if vw is BE:
    		v.back = min(v.back,w.discovertime)
}
```

没有桥 == 每一个点都有BE到根

---

# L14 - L15 图优化

Prim: 随机选一个点（初始化一下，dis[start_v]=-inf）向外找fringe，挑最短的边加进来，迭代器是已经找到的点集（sub-MST)，加边是fringe。
$$
T(n) =  n* extra Min+n* insert+m* delK
$$

---

MST

cut property --> 跨越Cut最轻的$\in$MST -->谈论cut是只看最轻的,加上它可构造MST 

cycle property -->属于Cycle中最重的$\notin$MST-->谈Cycle只看最重的，删去它可构造MS

---

dijkstra 

min-max

max-min(输油管道)

u-->v：dp[v] = max[( ][]dp[v],min(dp[u],w) [)][]

---

floyd

- 后继路由表，下一跳：GO\[i\]\[j\]=GO[i]\[k]
- 前驱路由表，上一跳：FROM\[i\]\[j\]=FROM[k]\[j]

all-pair max-min:

D\[i][j]=max( min(D\[i][k],D\[k][j]), D\[i][j] )

