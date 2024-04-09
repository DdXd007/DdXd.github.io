# Foyld最短路径

Foyld算法求最短路径的底层思想是，分别以每个点作为中介结点，不断去更新从一个点到另一个点的距离

使用Foyld算法首先需要解决建立邻接矩阵的问题，使用笔记中的方法建立一个Graph结构体储存图

```c++
/*使用图的数据结构*/
#define INF 0x3f3f3f3f3f3f3f3f
//选择0x3f3f3f3f3f3f3f3f作为INF而非0x7ffffffffffffffff是因为前者表示的INF与自生相加仍然大于题目的长度，符合无穷＋无穷仍为无穷的认知。而后者与自身相加会导致溢出，变成负数，不符合认知

const int MAXN = 405; //表示图中最大的顶点数
//无向图
typedef struct {
    ll vex[MAXN]; //顶点表
    ll arc[MAXN][MAXN]; //邻接矩阵
    ll vexnum; //顶点数
    ll arcnum; //边数
}Graph;


```

```c++
/*图的建立*/
Graph G; //建立图
ll n, m, q; //分别代表顶点数，边数，询问次数
    cin >> n >> m >> q;
    G.vexnum = n;
    G.arcnum = m;
    memset(G.arc, 0x3f, sizeof(G.arc)); //init邻接矩阵 将所有点之间的距离初始化为无穷大
    for(int i = 0; i <= n; i++) {
        G.arc[i][i] = 0;
    }

    for(int i = 0; i < m; i++) {
        ll u, v, w;
        cin >> u >> v >> w;
        //这里是一个坑点 题目中提及u和v之间存在一条长度为w的路，但是可能存在其他的路，所以只需要储存其中长度最短的一条即可
        G.arc[u][v] = min(G.arc[u][v], w);
        G.arc[v][u] = min(G.arc[v][u], w);
    }
```

```c++
/*Foyld算法本体*/
for(int k = 1; k <= n; k++) {  // k表示选取的中继节点
    for(int i = 1; i <= n; i++) { 
        for(int j = 1; j <= n; j++) {
            G.arc[i][j] = min(G.arc[i][j], G.arc[i][k] + G.arc[k][j]);
        }
    }
}
```

```c++
/*输出部分*/
while(q--) {
    int st, ed;
    cin >> st >> ed;
    if(G.arc[st][ed] == INF) {
        cout << "-1" << endl;
    }
    else {
        cout << G.arc[st][ed] << endl;
    }
}
```

路径记录部分还未学习