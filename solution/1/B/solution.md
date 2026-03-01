本题是较为复杂的模拟，考验数据结构的性质和应用。

队列( $queue$ )的性质是 $FIFO$ ，即先进先出。

我们将每一架飞机按照时间顺序入队，入队后根据现在飞机不断检查队首是否过期，出队，直到没有过期的飞机。

用这个方法，队首所留的一定是最久远但在新加入后仍然不过期的飞机。

因为国籍的数据范围允许，我们完全可以使用箱数组记录不同国籍数量。

```cpp
#include<cstdio>
#include<iostream>
#include<algorithm>
#include<queue>
using namespace std;

struct B {
    int t,k;
};

int v[100005];

int main() {
    queue<B> q;
    int n,cnt = 0;
    cin >> n;
    for (int i = 1;i <= n;i++) {
        int t,k;
        cin >> t >> k;
        for(int i = 1;i <= k;i++) {
            int x;
            cin >> x;
            q.push({t,x});
            v[x]++;
            if(v[x] == 1) cnt++;
            while(t - q.front().t >= 86400) {
                int tmp = q.front().k;
                q.pop();
                v[tmp]--;
                if (v[tmp] == 0) cnt--;
            }
        }
        cout << cnt << endl;
    }
    return 0;
}
```