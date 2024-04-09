# 数据结构：并查集（uset）

并查集是一种树形的数据结构，用于处理一些不相交集合的合并以及查询问题。比如查询一个森林中有几棵树，某个节点是否属于某棵树等问题。

### 主要构成

并查集由一个整型数组 `uset[]` 和两个函数 `find()` 、`join()` 构成。

`uset[]` 记录了每个节点的前驱节点

`find(x)` 函数用于查找指定节点 `x` 属于哪个集合

`join(x, y)` 函数用于合并两棵树。

```c++
/*初级版*/
const int maxn = 100;
typedef struct {
	vector<int> pa(maxn);
	
	int find(int son) {
        if(pa[son] == son) {
            return son;
        }
		return pa[son] = find(pa[son]); //路径压缩
	}

	void join(int a, int b) {
		int a_p = find(a);
		int b_p = find(b);
		if(a_p != b_p) {
			pa[a_p] = b_p;
		}
	}
} uset;


```

```c++
/*高级版（合并时考虑合并方式）*/

const int maxn = 100;
typedef struct {
    vector<int> pa(maxn);
    vector<int> size(maxn);

    int find(int son) {
        if(pa[son] == son) {
            return son;
        }
        return pa[son] = find(pa[son]);
    }
    bool join(int a, int b) {
        int a_p = uset.find(a);
        int b_p = uset.find(b);
        if(a_p != b_p) { //将比较小的树合并到较大的树
            if(size[a_p] >= size[b_p]) {
                pa[b_p] = a_p;
                size[a_p] += size[b_p];
            }
            else {
                pa[a_p] = b_p;
                size[b_p] += size[a_p];
            }
            return true;
        }
        return false;
    }

} uset;
```

