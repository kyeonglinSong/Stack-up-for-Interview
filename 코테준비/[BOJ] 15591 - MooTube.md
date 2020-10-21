# [BOJ] 15591 - MooTube



### 1. 풀이

- 사용한 자료구조 : 인접리스트
- 사용한 알고리즘 : BFS

내용은 재밌었지만 결국 시작점으로부터 모든 노드를 탐색하며, 경로에 있는 가중치의 최소값을 찾는 문제였다.

노드도 5000개밖에 없고, BFS를 사용하여 해결했다. 

  

### 2. 코드

```c++
#include <iostream>
#include <queue>
#include <cstring>
#include <vector>
using namespace std;

int n, q;
vector<pair<int, long long>> graph[5001];
long long check[5001];

typedef struct {
    int number;
    long long usado;
}node;

int bfs(long long k, int v)
{
    queue<node> q;
    q.push({v, 1000000000});
    check[v] = true;

    int result = 0;

    while(!q.empty())
    {
        node now = q.front();
        q.pop();

        for(int i=0 ; i<graph[now.number].size() ; i++)
        {
            int next_number = graph[now.number][i].first;
            long long temp_usado = graph[now.number][i].second;

            if(check[next_number] == -1)
            {
                long long next_usado = min(temp_usado, now.usado);
                check[next_number] = next_usado;
                if(next_usado >= k)
                    result++;
                q.push({next_number ,next_usado});
            }
        } 
    }
    return result;
}

int main()
{
    cin >> n >> q;
    memset(graph, 1000000000, sizeof(graph));
    for(int i=0 ; i<n-1 ; i++)
    {
        int from, to, usado;
        cin >> from >> to >> usado;
        graph[from].push_back(make_pair(to, usado));
        graph[to].push_back(make_pair(from, usado));
    }

    long long k;
    int v;
    for(int i=0 ; i<q ; i++)
    {
        memset(check, -1, sizeof(check));
        cin >> k >> v;
        cout << bfs(k, v) << "\n";
    }
}
```

