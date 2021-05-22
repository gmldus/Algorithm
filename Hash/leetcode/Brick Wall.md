### 554. Brick Wall
(주소)https://leetcode.com/problems/brick-wall/



#### 문제 요약:

최대한 벽돌을 지나지 않는 경우로 수직선을 그린다 할 때, 이 때 지나는 벽돌 개수를 구하는 문제

벽돌 하나하나가 끝나는 인덱스의 개수를 unordered_map으로 저장, 

row 개수인 n에서 map의 값이 가장 큰 map값을 빼면 정답.


#### 풀이 해설:



```c++
class Solution {
public:
    int leastBricks(vector<vector<int>>& wall) {
        unordered_map<int, int> mp;
        
        for(int i=0; i<wall.size(); i++){
            int index = 0;
            for(int j=0; j<wall[i].size()-1; j++){
                index+=wall[i][j];
                mp[index]++;
            }
        }
        
        int answer = 0;
        for(auto iter=mp.begin(); iter!=mp.end(); iter++){
            answer = max(answer, iter->second);
        }
        
        return wall.size() - answer;
    }
};
```
---
