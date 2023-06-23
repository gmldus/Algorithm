### 22. Generate Parentheses

(주소)https://leetcode.com/problems/generate-parentheses/



#### 문제 요약:

문자열을 만들어가는 도중에는 항상 열린 괄호 숫자 개수보다 닫힌 괄호 숫자 개수가 같거나 더 작아야한다.

그리고 열린 괄호의 개수는 최대 개수는 n개여야하기 때문에 이를 조건문에 포함해야한다.

마지막에 n * 2 길이의 문자열이 완성되었을 때는 열린 괄호 개수와 닫힌 괄호 개수가 같아야한다.

dfs로 모든 경우의 수를 탐색해가며 풀었다.

ex.

Input: n = 3

Output: ["((()))","(()())","(())()","()(())","()()()"]



#### 풀이 해설:

```javascript
function dfs(str, n, sum, output) {
    if (str.length === n * 2) {
        if (sum === 0) {
            output.push(str);
        }
        return;
    }

    if (sum !== n) {
        dfs(str + '(', n, sum + 1, output);
    }

    if (sum > 0) {
        dfs(str + ')', n, sum - 1, output);
    }
}
var generateParenthesis = function(n) {
    const output = [];
    dfs('', n, 0, output);
    return output;
}
```
---

예전 코드

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
