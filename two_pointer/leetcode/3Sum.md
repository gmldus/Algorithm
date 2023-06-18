### 15. 3Sum

(주소)[https://leetcode.com/problems/combination-sum/](https://leetcode.com/problems/3sum/)



#### 문제 요약:

3개의 숫자를 골랐을 때 그 합이 0이 되는 숫자 조합들을 구하는 문제

단, 동일한 숫자의 조합은 중복되면 안됨

Ex.

Input: nums = [-1,0,1,2,-1,-4]

Output: [[-1,-1,2],[-1,0,1]]

Explanation: 

nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.

nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.

nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.

The distinct triplets are [-1,0,1] and [-1,-1,2].

Notice that the order of the output and the order of the triplets does not matter.


#### 풀이 해설:
모든 숫자들의 조합을 다 구하기는 비효율적이니까 우선 숫자 배열을 크기 순으로 정렬한다.
3개의 숫자를 잡고 더해봐야하기 때문에 맨 앞 숫자를 하나씩 잡으면서 나머지 2개는 뒤쪽에서 two pointer로 잡아서 더해본다.

합이 0이 되면 이를 result 배열에 추가한다.
그리고 left를 하나 뒤로, right를 하나 앞으로 이동시킨다.

합이 0보다 작으면 left pointer를 하나 뒤로 당기고 반대의 경우엔 right pointer를 앞으로 하나 당긴다.

!! 그런데 정답에 중복이 있으면 안되기 때문에 합이 0이 되면 result 배열에 추가하고 난 뒤 left 뒤에 똑같은 숫자가 있는지 right 앞에 똑같은 숫자가 있는지 확인하고
똑같은 숫자면 다른 숫자가 나올 때까지 각각 뒤, 앞으로 이동시켜서 건너뛰게 한다.

그리고 첫번째 숫자도 지정할 때 바로 뒤에 똑같은 숫자면 다른 숫자가 나올 때까지 건너뛴다.


```javascript
var threeSum = function(nums) {
    const result = [];

    nums.sort((a,b) => a - b);

    let sum = 0;
    for (let i = 0; i < nums.length - 2; i++) {
        let left = i + 1;
        let right = nums.length - 1;
      
        while(left < right) {
            sum = nums[i] + nums[left] + nums[right];

            if (sum === 0) {
                result.push([nums[i], nums[left], nums[right]]);
                while(left < right && nums[left] === nums[left + 1]) { // to avoid duplication
                    left++;
                }
                left++;

                while(left < right && nums[right] === nums[right - 1]) { // to avoid duplication
                    right--;
                }
                right--;
            } else if (sum < 0) {
                left++;
            } else {
                right--;
            }
        }

        while(i < nums.length - 3 && nums[i] === nums[i + 1]) { // to avoid duplication
            i++;
        } 
    }

    return result;
};
```
---
