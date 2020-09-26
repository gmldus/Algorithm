### 332. Reconstruct Itinerary

(주소)https://leetcode.com/problems/reconstruct-itinerary/



#### 문제 요약:

"JFK" 에서 시작하여서 존재하는 경로를 따라 사전식 순서가 가장 빠른 경로를 출력하는 문제.


#### 풀이 해설:

1. priority queue를 오름차순으로 선언하는 법을 알아냈다.

```c++
priority_queue<자료형, vector<자료형>, greater<자료형>>
```
2. 깊이우선탐색을 더 공부해야할 것 같다.

    처음에는 모든 가능한 경로를 찾아서 정렬한 다음, 그 중 사전순으로 가장 빠른 vector<string>을 출력하려했다. ㅎㅏ지만 시간초과
    
    그래서 다른 코드를 참고해서 일단 거슬러 올라가며 vector에 값을 넣은 다음 마지막에 reverse 해주는 코드로 구현했다.
    
    이미 지나간 경로를 체크하려 처음엔 visited 개념을 사용하려했지만 그냥 graph에서 사용된 경로를 삭제해주면 된다. ( & destinations  인 이유.)
    

```c++
class Solution {
public:
    vector<string> answer;
    map<string, priority_queue<string, vector<string>, greater<string>>> graph;
    
    void dfs(string place){
        auto & destinations = graph[place];
        while(!destinations.empty()){
            string picked = destinations.top();
            destinations.pop();
            dfs(picked);
        }
        answer.push_back(place);
    }
    
    vector<string> findItinerary(vector<vector<string>>& tickets) {
        for(int i=0;i<tickets.size();i++){
            graph[tickets[i][0]].push(tickets[i][1]);
        }
        
        dfs("JFK");
        reverse(answer.begin(), answer.end());
        return answer;
    }
};
```
---
