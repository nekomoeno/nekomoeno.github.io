+++

title = '算法练习 前缀和与差分'
date = 2024-08-31T20:42:21+08:00
draft = false
tags = [ "算法", "牛客" ]
author = "Nekomoeno"

showToc = true
TocOpen = false
hidemeta = false
comments = false
description = "Desc Text."

disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true

[cover]
image = "<image path/url>"
alt = "<alt text>"
caption = "<text>"
relative = false
hidden = true

+++

[TOC]

### [值周][https://ac.nowcoder.com/acm/problem/24636] - 差分

#### 题目描述:

   JC内长度为L的马路上有一些值周同学，每两个相邻的同学之间的间隔都是1米。我们可以把马路看成一个数轴，马路的一端在数轴0的位置，另一端在L的位置；数轴上的每个整数点，即0,1,2,…L，都有一个值周同学。 由于水宝宝有用一些区间来和ssy搞事情，所以为了避免这种事走漏风声，水宝宝要踹走一些区域的人。这些区域用它们在数轴上的起始点和终止点表示。已知任一区域的起始点和终止点的坐标都是整数，区域之间可能有重合的部分。现在要把这些区域中的人（包括区域端点处的两个人）赶走。你的任务是计算将这些人都赶走后，马路上还有多少个人。  

#### 输入描述:

> 第一行有2个整数L和M，L代表马路的长度，M代表区域的数目，L和M之间用一个空格隔开。 接下来的M行每行包含2个不同的整数，用一个空格隔开，表示一个区域的起始点和终止点的坐标

#### 输出描述:

> 1个整数，表示马路上剩余的人的数目。

#### 示例1

**输入**

```
500 3
150 300
100 200
470 471
```

**输出**

```
298
```

#### 说明

> 对于所有的数据，1 ≤ L ≤ 100000000
>
> 对于10%的数据，1 <= M <= 100
>
> 对于20%的数据，1 <= M <=1000
>
> 对于50%的数据，1 <= M <=100000
>
> 对于100%的数据，1 <= M <=1000000

#### 参考代码：

```C++
#include <iostream>

using namespace std;

const int N = 100000010;

int a[N], sum, ans;

int main(){
    ios_base::sync_with_stdio(0); cin.tie(0);cout.tie(0);
    
    int n, m; cin >> n >> m;
    
    for(int i = 0; i < m; i ++){
        int st, ed; cin >> st >> ed;
        a[st] += 1;
        a[ed + 1] -= 1;
    }
    for(int i = 0; i <= n; i ++){
        sum += a[i];
        if(sum == 0) ans++;
    }
    
    cout << ans << endl;
    
    return 0;
}
```



### [中位数图][https://ac.nowcoder.com/acm/problem/19913] - 前缀和

#### 题目描述                    

给出 1 ~ n 的一个排列，统计该排列有多少个长度为奇数的连续子序列的中位数是b。中位数是指把所有元素从小到大排列后，位于中间的数。

#### 输入描述:

> 第一行为两个正整数 n 和 b ，第二行为 1 ~ n 的排列。

#### 输出描述:

> 输出一个整数，即中位数为 b 的连续子序列个数。

#### 示例1                        

**输入**

```
7 4
5 7 2 4 3 1 6
```

**输出**

```
4
```

#### 备注:

>对于30%的数据中，满足 n ≤ 100;
>
>对于60%的数据中，满足 n ≤ 1000;
>
>对于100%的数据中，满足 n ≤ 100000, 1 ≤ b ≤ n。

#### 参考代码：

```C++
#include <iostream>
#include <unordered_map>

using namespace std;

const int N = 100010;
int a[N];
unordered_map<int,int> occ;

int main() {
    int n, b; cin >> n >> b;
    int pos = -1;
    for(int i = 0; i < n; i++) {
        int t; cin >> t;
        if(t > b) a[i] = 1;
        else if(t < b) a[i] = -1;
        else pos = i;
    }
    int sum = 0, ans = 1, cur;
    for(cur = pos - 1; cur >= 1; --cur) {
        sum += a[cur];
        occ[sum]++;
        if(sum == 0) ans++;
    }
    sum = 0;
    for(cur = pos + 1; cur < n; ++cur) {
        sum += a[cur];
        ans += occ[-sum];
        if(sum == 0) ans++;
    }
    
    cout << ans << endl;
    
    return 0;
}
```

