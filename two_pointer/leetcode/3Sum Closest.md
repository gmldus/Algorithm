### 16. 3Sum Closest

(주소)[https://leetcode.com/problems/combination-sum/
](https://leetcode.com/problems/3sum-closest/)


#### 문제 요약:

3개의 숫자를 골랐을 때 그 합이 target과 가장 근접한 경우의 합을 구하는 문제

Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).


#### 풀이 해설:
모든 숫자들의 조합을 다 구하기는 비효율적이니까 우선 숫자 배열을 크기 순으로 정렬한다.
3개의 숫자를 잡고 더해봐야하기 때문에 맨 앞 숫자를 하나씩 잡으면서 나머지 2개는 뒤쪽에서 two pointer로 잡아서 더해본다.

이때까지의 값보다 더 근접한 합이 나오면 이걸로 업데이트를 한다.

더했을 때 target보다 작으면 target에 더 근접하기 위해서는 합이 더 커져야하기 때문에 left point를 하나 뒤로 당긴다.
반대의 경우엔 right point를 앞으로 하나 당긴다.


```javascript
var threeSumClosest = function(nums, target) {
    nums.sort((a,b) => a - b);

    let output;
    let min = 10000;
    let sum;
    for (let i = 0; i < nums.length - 2; i++) {
        let left = i + 1;
        let right = nums.length - 1;

        while(left < right) {
            sum = nums[i] + nums[left] + nums[right];

            if (output === undefined || Math.abs(target - sum) < min) {
                min = Math.abs(target - sum);
                output = sum;
            }

            if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }

    return output;
};
```
---
