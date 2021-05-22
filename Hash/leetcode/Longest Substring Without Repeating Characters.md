### 3. Longest Substring Without Repeating Characters
(주소)https://leetcode.com/problems/longest-substring-without-repeating-characters/



#### 문제 요약:

중복없는 연속된 문자열의 최대 길이 구하는 문제

two pointer 개념으로 풀고 원소의 존재 유무는 hash table (unordered_map)으로 알아냄.


#### 풀이 해설:



```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<int,int> mp;
        queue<int> q;
        int answer = 0, cnt = 0;
        
        for(int i=0; i<s.size(); i++){
            if(mp.count(s[i])) {
                answer = max(answer, cnt);
                
                while(1){
                    int c = q.front();
                    
                    q.pop(); 
                    mp.erase(c);
                    cnt--;
                    
                    if(c == s[i]) break;
                }
            }
            cnt++;
            mp[s[i]]++;
            q.push(s[i]);
        }
        
        answer = max(answer, cnt);
        return answer;
    }
};
```
---
