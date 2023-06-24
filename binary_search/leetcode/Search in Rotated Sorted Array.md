### 33. Search in Rotated Sorted Array


(주소)[https://www.acmicpc.net/problem/3079](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)


#### 문제 요약:

Rotated Sort 상태의 array에서 target이 몇번째 인덱스에 있는지 O(log n) 복잡도로 찾는 문제.

EX.

Input: nums = [4,5,6,7,0,1,2], target = 0

Output: 4

#### 풀이 해설:

O(log n)때문에 binary searh로 풀었음

Rotated Sorted인 점을 고려하여 target이 어디에 있을지 예측


```javascript
var search = function(nums, target) {
    let output;
    let mid;
    let start = 0;
    let end = nums.length - 1;

    while(start <= end) {
        mid = Math.floor((start + end) / 2);
        if (nums[mid] === target) {
            output = mid;
            break;
        }

        if (nums[start] <= nums[mid]) {
            if (target >= nums[start] && target < nums[mid]) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        } else {
            if (target < nums[start] && target > nums[mid]) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
    }

    return output ?? -1;
};
```
---
