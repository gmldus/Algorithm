### 55. Jump Game
(주소)https://leetcode.com/problems/jump-game/



#### 문제 요약:

각 자리에서 점프해서 이동할 수 있는 칸의 개수를 담은 nums 배열이 주어지고

가장 마지막 칸에 도달할 수 있는지 여부를 반환하는 문제.

#### 풀이 해설:

최대로 어디까지 도달할 수 있는지를 담은 maxIndex 변수가 있고

만약 현재 검사하는 칸의 인덱스(i)가 현재까지 기록해둔 maxIndex보다 같거나 작다면 그 칸에서 더 이동할 수 있다는 뜻이기 때문에

그 칸에서 최대로 이동할 수 있는 인덱스와 현재까지의 maxIndex를 비교해서 더 큰 값으로 maxIndex를 업데이트 한다.

최종적으로는 maxIndex가 가장 마지막 칸의 인덱스(nums.size()-1)랑 같거나 더 크다면 true를 반환한다.

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int maxIndex = 0;
        
        for(int i=0;i<nums.size();i++){
            if(maxIndex>=i){
                maxIndex = max(maxIndex, i+nums[i]);
            }
        }
        
        return maxIndex >= nums.size()-1;
    }
};
```
---
