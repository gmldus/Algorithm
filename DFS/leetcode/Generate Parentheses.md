### 22. Generate Parentheses

(주소)https://leetcode.com/problems/generate-parentheses/



#### 문제 요약:

괄호 짝이 맞는 문자열을 모두 찾는다.

이런 괄호짝 문제 같은 경우는 cnt 수로 측정하기 보다는 열린괄호 개수(left) 닫는괄호 개수(right)를 따로 가져가면서 dfs를 구현했다.

well-formed 한 괄호쌍을 만드려면 항상 열린괄호가 닫힌괄호 개수보다 많은 상태일 때만 닫힌 괄호를 붙여야 한다. ✅


#### 풀이 해설:



```c++
class Solution {
public:
    int N;
    vector<string> answer;
    
    void dfs(string s, int left, int right){
        if(left==N && right==N){
            answer.push_back(s);
            return;
        }
        if(left<N){
            dfs(s+'(', left+1, right);
        }
        if(right<N && left>right){
            dfs(s+')', left, right+1);
        }
    }
    
    vector<string> generateParenthesis(int n) {
        N=n;

        dfs("", 0, 0);
        return answer;
    }
};
```
---
