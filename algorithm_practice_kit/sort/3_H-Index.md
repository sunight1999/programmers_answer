## 코드
``` c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    /* 1 */
    sort(citations.begin(), citations.end(), greater<int>());
    
    int i;
    for (i = 0; i < citations.size(); ++i)
    {
        /* 2 */
        if (i + 1 >= citations[i])
            return i < citations[i] ? i + 1 : i;
    }
    
    /* 3 */
    return i;
}
```

## 풀이
**1. 내림차순 정렬**  
가장 큰 h-index를 찾아야하므로 `citations`를 내림차순 정렬한다.

**2. H-Index 판별**  
`citations`의 값을 내림차순으로 정렬했으므로 `i + 1`은 인용 수가 현재 탐색 중인 논문의 인용 수(`citations[i]`)보다 같거나 많은 논문의 수이다.
따라서 `i + 1 >= citations[i]` 조건에 걸렸다면, citations[i]가 최소한의 h-index가 될 수 있다는 의미다.

다만, `[7, 6, 5, 5, 3, 1]`과 같은 경우, 위 조건에 걸렸을 때의 citations[i]인 3보다 i가 4로 더 큰데, 이 경우 인용 횟수가 <<<<<ㅗㄷㄱㄷ>>>>

```
citations = [7, 6, 3, 1]
i = 0 : 인용 수가 7 이상인 논문 수 = i + 1 = 1
i = 1 : 인용 수가 6 이상인 논문 수 = i + 1 = 2
i = 2 : 인용 수가 3 이상인 논문 수 = i + 1 = 3 <<<<--- (i + 1 = 3)이 (citations[i] = 3)보다 크거나 같으므로 h-index의 가능성이 생김
```
