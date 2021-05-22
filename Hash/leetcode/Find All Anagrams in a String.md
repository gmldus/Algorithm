### 438. Find All Anagrams in a String
(주소)https://leetcode.com/problems/find-all-anagrams-in-a-string/



#### 문제 요약:

anagram이 시작하는 인덱스들을 모두 구하는 문제.

Sliding Window 알고리즘 개념이 들어가고 

anagram (순서만 바뀐 문자열) 인지는 unordered_map을 이용해서 알아냈다. ( isEqual 함수 )

#### 풀이 해설:



```c++
class Solution {
public:
    bool isEqual(unordered_map<char,int> mp, unordered_map<char,int> mp2) {
        for(auto iter=mp.begin();iter!=mp.end();iter++){
            if(!mp2.count(iter->first) || mp2[iter->first] != iter->second) return false;
        }
        return true;
    }
    
    vector<int> findAnagrams(string s, string p) {
        int index = 0;
        unordered_map<char,int> mp;
        unordered_map<char,int> mp2;
        vector<int> answer;
        
        int n = p.size();
        
        for(int i=0; i<n; i++){
            mp[p[i]]++;
        }
        
        for(int i=0; i<s.size(); i++){
            mp2[s[i]]++;
            if(i>=n) mp2[s[i-n]]--;
            
            if(isEqual(mp, mp2)){
                answer.push_back(i-n+1); // anagram의 시작 인덱스
            }
        }
        
        return answer;
    }
};
```
---
