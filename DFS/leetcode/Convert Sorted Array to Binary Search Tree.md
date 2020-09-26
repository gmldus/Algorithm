### 108. Convert Sorted Array to Binary Search Tree

(주소)https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/



#### 문제 요약:

정렬된 배열의 원소들을 이용해서 이진탐색트리 를 만드는 문제이다.

핵심은 **이진탐색** 방법을 따르는데 이를 **재귀**로 푸는 것이다.

재귀로 Treenode를 아래에서부터 위로 거슬러 올라가며 덧붙이는 코드이다. (헤매었으므로 이런 구조에 익숙해질 것 !)


#### 풀이 해설:



```c++
class Solution {
public:
    
    TreeNode* dfs(int left, int right, vector<int>& nums){
        if(left>right) return NULL;
        int idx = (left+right)/2;
        TreeNode* node = new TreeNode(nums[idx]);
        
        node->left = dfs(left, idx-1, nums);
        node->right = dfs(idx+1, right, nums);

        return node;
    }
    
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        TreeNode* answer = dfs(0, nums.size()-1, nums);
        return answer;
    }
};
```
---
