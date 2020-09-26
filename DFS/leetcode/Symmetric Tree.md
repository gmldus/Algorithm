### 101. Symmetric Tree

(주소)https://leetcode.com/problems/symmetric-tree/



#### 문제 요약:

트리의 노드가 mirror로 보았을 때 처럼 대칭인지 확인하는 문제.


#### 풀이 해설:

노드들을 탐색했다.

트리를 루트노드 기준으로 반으로 자른다 생각하고, 

왼쪽 트리는 왼쪽 -> 오른쪽 노드 순으로 탐색하고, 오른쪽 트리는 오른쪽 -> 왼쪽 노드 순으로 탐색하도록 헸다.

탐색하면서 만나는 node 값들을 벡터에 넣어두고 마지막에 두개의 벡터 값이 순서대로 모두 동일한지 확인하여 동일하다면 true를 리턴한다.

```c++
class Solution {
public:
    vector<int> v1;
    vector<int> v2;
    
    void dfs_left(TreeNode* node){
        v1.push_back(node->val);
        
        if(node->left) dfs_left(node->left);
        if(!node->left) v1.push_back(-1);  // 주의!! : null을 만날 때도 null이라는 값을 넣어줘야한다. 
        if(node->right) dfs_left(node->right);
        if(!node->right) v1.push_back(-1);
    }
    
    void dfs_right(TreeNode* node){
        v2.push_back(node->val);
        
        if(node->right) dfs_right(node->right);
        if(!node->right) v2.push_back(-1);
        if(node->left) dfs_right(node->left);
        if(!node->left) v2.push_back(-1);
    }
    
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        if(!root->left && !root->right) return true;
        if(!root->left && root->right) return false;
        if(root->left && !root->right) return false;
        
        dfs_left(root->left);
        dfs_right(root->right);

        for(int i=0;i<v1.size();i++){
            if(v1[i]!=v2[i]) return false;
        }
        return true;
    }
};
```
---
