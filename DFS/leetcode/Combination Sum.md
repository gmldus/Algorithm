### 39. Combination Sum

(주소)https://leetcode.com/problems/combination-sum/



#### 문제 요약:

candidates에 있는 숫자를 여러번 사용할 수 있기 때문에 앞에서부터 연속으로 같은 숫자(같은 인덱스의 숫자)를 더해나간다.

sum이 target보다 커지면 리턴하고, 더할 숫자의 index를 하나 올려 더해나가본다.

ex.

candidates = [2,3,5], target = 8

v : [3,3] -> [3,3,3](if 문에서 걸리기 때문에 생략)  -> [3,5]


#### 풀이 해설:



```c++
class Solution {
public:
    vector<vector<int>> answer;
    
    void dfs(int sum, int index, vector<int> v, int target, vector<int>& candidates){
        if(sum==target){
            answer.push_back(v);
            return;
        }
        if(sum>target){
            return;
        }
        for(int j=index;j<candidates.size();j++){
            vector<int> vv=v;
            vv.push_back(candidates[j]);
            if(sum+candidates[j]<=target) dfs(sum+candidates[j], j, vv, target, candidates);  // 더해서 target보다 크다면 굳이 안간다. 어짜피 막고있기 때문
            vv.pop_back();
        }
    }
    
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int>v;
        dfs(0,0,v,target,candidates);
        return answer;
    }
};
```
---
