### 45. Jump Game II
(주소)https://leetcode.com/problems/jump-game-ii/



#### 문제 요약:

각 자리에서 점프해서 이동할 수 있는 칸의 개수를 담은 nums 배열이 주어지고

가장 마지막 칸에 도달할 수 있다고 보장된다는 가정 하에

최대한 빨리 점프 몇 번만에 도달할 수 있는지 구하는 문제.

#### 풀이 해설:

해당 칸까지 최소 몇 번의 점프로 올 수 있는지를 기록하는 minReach라는 벡터를 선언했다.

첫 칸의 minReach 값은 항상 0이며 나머지 칸들은 -1로 초기화한다.

점프해서 도착하는 칸이 처음 도달하는 칸이라면 (= minReach 값이 -1)  -> 어짜피 먼저 체크되는 값이 항상 최솟값이다.

점프하기 시작한 칸의 minReach값에서 1을 더한 값으로 점프되는 칸의 minReach 값을 세팅한다.

마지막 칸의 minReach 값이 정답.

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        vector<int> minReach;
        
        for(int i=0;i<nums.size();i++){
            minReach.push_back(-1);
        }
        
        minReach[0]=0;
        
        for(int i=0;i<nums.size();i++){
            int start = minReach[i];

            for(int j=1;j<=nums[i];j++){
                if(i+j<nums.size() && minReach[i+j]==-1){
                    minReach[i+j]=start+1;
                }
            }
        }
        
        return minReach[nums.size()-1];
    }
};
```
---
