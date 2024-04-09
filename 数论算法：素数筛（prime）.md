# 数论算法：素数筛（prime）

## 1、朴素筛法

时间复杂度O（）

```c++
Const int maxn  = 1e5 + 10;
bool is_prime[maxn];

void init_prime() {
	memset(is_prime, true, sizeof(is_prime));
	is_prime[0] = is_prime[1] = false;
	for(int i = 2; i < maxn; i++) {
		if(is_prime[i]) {
			for(int j = 2 * i; j < maxn; j += i) {
				is_prime[j] = false;
			}
		}
	}
}
```

## 2、埃氏筛法

时间复杂度：O(n log log n)

```c++
const int maxn = 1e6 + 10;
bool is_prime[maxn];

void init_prime() {
    memset(is_prime, true, sizeof(is_prime));
    is_prime[0] = is_prime[1] = false;
    for(int i = 2; i < maxn; i++) {
        if(is_prime[i]) {
            for(int j = 2; j * i < maxn; j++) {
                is_prime[i * j] = false;
            }
        }
    }
}
```

## 3、欧拉筛法

时间复杂度：O(n)

```c++
const int maxn = 1e8 + 10;
int prime[maxn], primeSize = 0;
bool not_prime[maxn]; //标记下标数字是否被筛

void init_prime() {
    not_prime[0] = not_prime[1] = true;
    for(int i = 2; i < maxn; i++) { //主循环，遍历
        if(!not_prime[i]) prime[primeSize++] = i;
        for(int j = 0; j < primeSize && i * prime[j] < maxn; j++) {
            not_prime[i * prime[j]] = true;
            if(i % prime[j] == 0) break;
        }
    }
}
```

