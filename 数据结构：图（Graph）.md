# 数据结构：图（Graph）

[数据结构：图(Graph)【详解】_数据结构graph类-CSDN博客](https://blog.csdn.net/Real_Fool_/article/details/114141377?ops_request_misc=%7B%22request%5Fid%22%3A%22170859426616800226561562%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170859426616800226561562&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-114141377-null-null.142^v99^pc_search_result_base3&utm_term=图&spm=1018.2226.3001.4187)

### 【知识框架】

![](E:\笔记\数据结构：图（Graph）\image\知识导图.png) 

----

### 图的基本概念

在线性表中，数据元素之间是被串起来的，仅有线性关系，每个数据元素只有一个直接前驱和一个直接后继。在树形结构中，数据元素之间有着明显的层次关系，并且每一层上的数据元素可能和下一层中多个元素相关，但只能和上一层中一个元素相关。图是一种较线性表和树更加复杂的数据结构。在图形结构中，结点之间的关系可以是任意的，图中任意两个数据元素之间都可能相关。

-----



## 一、图的定义

图(Graph)是由顶点的有穷非空集合`V ( G )`和顶点之间边的集合`E ( G ) `组成，通常表示为: `G = ( V , E )` `G=(V,E)G=(V,E)`，其中，G 表示个图，V 是图G 中顶点的集合，E 是图 G 中边的集合。若 `V = {v1, v2, ..., vn}` `V= {v_1, v_2,...,v_n}` `V={v1, v2, ..., vn}`，则用 |V|表示图G中顶点的个数，也称图G的阶，E = { ( u , v ) ∣ u ∈ V , v ∈ V } E= \{(u, v) |u∈V, v∈V\} E={(u,v)∣u∈V,v∈V}，|E|表示图G中边的条数。




## 二、图的基本概念和术语

### 1、有向图

​	若E是有向边(也称弧)的有限集合时，则图G为有向图。弧是顶点的有序对，记为<v, w>，其中v,w是顶点，v称为弧尾，w称为弧头，<v,w>称为从顶点v到顶点w的弧，也称v邻接到w，或w邻接自v。![](E:\笔记\数据结构：图（Graph）\image\20210227111745661.png)


### 2、无向图

### 3、简单图

### 4、多重图

### 5、完全图

### 6、子图

### 7、连通、连通图和连通分量

### 8、强连通图、强连通分量

### 9、生成树、生成森林

### 10、顶点的度、入度和出度

### 11、边的权和网

### 12、稠密度、稀疏图

### 13、路径、路径长度和回路

### 14、简单路径、简单回路

### 15、距离

### 16、有向树



## 二、图的储存

![](E:\笔记\数据结构：图（Graph）\image\b520e3039b8e4152ba79f78f72fd464d.png)

### 1、邻接矩阵

```c++
#include <bits/stdc++.h>
#define MAXN 200
#define INF __INT_MAX__
using namespace std;

//无向图
typedef struct {
    int vex[MAXN]; //顶点表
    int arc[MAXN][MAXN]; //邻接矩阵
    int vexnum; //顶点数
    int arcnum; //边数
}Graph;
void cgra(Graph &G) { //创建无向图
    cin >> G.vexnum >> G.arcnum;
    //inti 初始化邻接矩阵
    for(int i = 0; i <= G.vexnum; i++) { 
        //memset的时间复杂的是O(n)
        memset(G.arc[i], 0, G.vexnum * sizeof(int));
    }
    for(int i = 1; i <= G.vexnum; i++) {
        cin >> G.vex[i];
    }
    //创建连接关系
    for(int i = 0; i < G.arcnum; i++) {
        int tmp1, tmp2;
        cin >> tmp1 >> tmp2;
        G.arc[tmp1][tmp2] = 1;
        G.arc[tmp2][tmp1] = 1;
    }
}
```

### 2、邻接表

```c++
#include <bits/stdc++.h>
using namespace std;

typedef struct {
    vector<int> V;
    vector<vector<int>> E;
    int vNum;
    int eNum;
}Graph;
void cgra(Graph &G) {
    cin >> G.vNum >> G.eNum;
    G.V.resize(G.vNum + 1);
    G.E.resize(G.vNum + 1);
    for(int i = 1; i <= G.vNum; i++) {
        cin >> G.V[i];
    }
    for(int i = 0; i < G.eNum; i++) {
        int tmp1, tmp2;
        cin >> tmp1 >> tmp2;
        G.E[tmp1].push_back(tmp2);
        G.E[tmp2].push_back(tmp1);
    }
}
```

### 3、十字链表

是一种整合了邻接表和逆邻接表的链状（网状）表

### 4、邻接多重表

升级版邻接表

### 5、边集数组

记录边的连接关系的表格



## 三、图的遍历

均使用邻接表演示

### 一、深度优先遍历（DFS）

一般使用递归的方式实现

```c++
vector<int> dfs_vis(MAXN, 0);
void dfs(Graph g, int step) {
    //cout << g.V[step] << ' ';
    dfs_vis[step] = 1;
    for(int i = 0; i < g.E[step].size(); i++) {
        int son = g.E[step][i];
        if(dfs_vis[son] == 0) {
            dfs(g, son);
        }
    }
}
```

### 二、广度优先遍历（BFS）

一般使用队列queue实现

```c++
vector<int> bfs_vis(MAXN, 0);
void bfs(Graph g, int step) {
    queue<int> q;
    q.push(step);
    bfs_vis[step] = 1;
    while(q.empty() == 0) {
        int cur = q.front();
        q.pop();
        //cout << cur << ' ';
        for(int i = 0; i < g.E[cur].size(); i++) {
            int son = g.E[cur][i];
            if(bfs_vis[son] == 0) {
                q.push(son);
                bfs_vis[son] = 1;
            }
        }
    }
}
```

###  三、图的遍历与图的连通性

遍历过的元素数与总的元素数

## 四、最小生成树

一个连通图的生成树是一个极小的连通子图，它含有图中全部的顶点，但只有足以构成一棵树的``n − 1``条边，若砍去它的一条边，则会使生成树变成非连通图；若给它增加一条边，则会形成图中的一条回路。对于一个带权连通无向图``G = ( V , E )``，生成树不同，其中边的权值之和最小的那棵生成树（构造连通网的最小代价生成树），称为G的最小生成树(Minimum-Spanning-Tree, MST)。

### 一、普里姆（Prim）算法

### 二、克鲁斯卡尔（Kruskal）算法



## 五、最短路径

### 一、迪杰斯特拉（Dijkstra）算法

### 二、弗洛伊德算法



## 六、拓扑排序



## 七、关键路径



