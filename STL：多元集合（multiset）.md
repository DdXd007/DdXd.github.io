# STL：多元集合（multiset）

multiset 是 \<set\> 中的一个非常有用的类型，包含在<bits/stdc++.h>中，可以将它看作一个序列，插入、删除一个数都能在O(logn)内完成，而且它可以保证序列中的元素时刻是有序的，而且允许序列中存放重复的数。

## 使用方法

```c++
multiset<int> mst;				//建立一个multiset
for(int i = 0; i < 10; i++) {
	int tmp;cin >> tmp;			
    mst.insert(tmp);			//插入元素
}
for(auto it : mst) {
	cout << it << ' '; 			//利用迭代器遍历
}
cout << endl;
```

类似地，multiset可以储存其他类型（string、double、···）和自定义类型（struct).在使用自定义结构类型时需要写cmp函数或者在结构体内重载小于号。

例如，结构体：

```c++
typedef struct stru {
	int x;
	int y;
} stru;
```

在结构体内重载小于号

```c++
typedef struct stru {
	int x;
	int y;
    
    bool operator < (const stru t) const {
		if(x != t.x) {
			return x < t.x;
        }
        return y < t.y;
    }
} stru;
```

## 内置操作

| 操作           | 效果                     |
| -------------- | ------------------------ |
| mst.size()     | 返回当前元素数量         |
| mst.empty()    | 判断集合是否为空         |
| mst.max_size() | 返回最大能容纳元素的个数 |
| mst1 == mst2   | 判断集合是否相等         |
| mst1 != mst2   | 判断集合是否不等         |
| mst1 < mst2    | 判断集合是否小于         |
| mst1 > mst2    | 判断集合是否大于         |
| mst1 <= mst2   | 判断集合是否小于等于     |
| mst1 >= mst2   | 判断集合是否大于等于     |

## 内置搜索函数

在搜索元素时应当优先考虑使用内置的函数。

| 操作              | 效果                                            |
| ----------------- | ----------------------------------------------- |
| count(elem)       | 返回元素值为elem的个数                          |
| find(elem)        | 返回元素值为elem的第一个函数，没有就返回end（） |
| lower_bound(elem) | 返回元素值 >=elem的第一个元素的位置（迭代器）   |
| upper_bound(elem) | 返回元素值 > elem的第一个元素的位置（迭代器）   |
| equal_range(elem) | 返回元素值为elem的第一个位置和最后一个位置      |

## 赋值

| 操作             | 效果             |
| ---------------- | ---------------- |
| mst1 = mst2      | 将mst2赋值给mst1 |
| mst1.swap(mst2)  | 交换mst1和mset2  |
| swap(mst1, mst2) | 效果同上         |

## 迭代器相关操作

​	set和multiset都支持双向迭代器，在迭代器操作中所有元素被视为常数，无法修改元素值，从而破坏内部结构。

| 操作         | 效果                                                         |
| ------------ | ------------------------------------------------------------ |
| mst.begin()  | 返回指向第一个元素的迭代器                                   |
| mst.end()    | 返回指向最后一个元素的下一个位置的迭代器                     |
| mst.rbegin() | 返回一个逆向迭代器，指向逆向迭代器的第一个元素               |
| mst.rend()   | 返回一个逆向迭代器，指向逆向迭代器的最后一个元素的下一个位置 |

## 插入和删除元素

| 操作                  | 效果                                                 |
| --------------------- | ---------------------------------------------------- |
| mst.insert(elem)      | 插入一个elem副本，返回新元素位置，无论插入成功与否。 |
| met.insert(pos, elem) | 安插一个elem元素副本，返回新元素位置，提升插入速度   |
| mst.insert(beg, end)  | 将区间[beg, end)所有元素安插到c，无返回值            |
| mst.erase(elem)       | 删除与elem相等的所有元素，返回被移除的元素个数       |
| mst.erase(pos)        | 移除迭代器pos所指位置的元素，无返回值                |
| mst.erase(beg, end)   | 移除区间[beg, end)所有元素，无返回值                 |
| mst.clear()           | 移除所有元素，将容器清空                             |

