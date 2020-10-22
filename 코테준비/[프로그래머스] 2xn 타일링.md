# [프로그래머스] 2xn 타일링



### 1. 구조

- 사용한 자료구조 : 인접행렬
- 사용한 알고리즘 : bottom-up dp

그냥 그냥 피보나치 수랑 똑같다. 

dp문제는 항상 어려워보이지만 점화식을 찾으면 쉽게 풀린다. 점화식 찾기가 어려워서 그렇지..

  

### 2. 알고리즘

arr[i] = arr[i-1] + arr[i-2]

  

### 3. 코드

```c++
#include <string>
#include <vector>

using namespace std;
long long arr[60001];

int dfs(int n)
{
    arr[1] = 1;
    arr[2] = 2;
    for(int i=3 ; i<=n ; i++)
    {
        arr[i] = ((arr[i-1]) + arr[i-2])%1000000007;
    }
    return arr[n];
}

int solution(int n) 
{
    return dfs(n);
}
```





