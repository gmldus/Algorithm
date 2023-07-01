### 53. Maximum Subarray

(주소)[https://leetcode.com/problems/combination-sum/](https://leetcode.com/problems/maximum-subarray/description/)



#### 문제 요약:

합이 최대인 sub array의 합을 구하는 문제이다.


ex.

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]

Output: 6

Explanation: The subarray [4,-1,2,1] has the largest sum 6.


#### 풀이 해설:

1. 최대 합만 구하면 되기 때문에 계속해서 비교하여 최댓값을 갱신시켜나간다.

2. 양수들로 이루어진 sub array가 항상 최대 합인건 아니다. 중간에 음수가 나오더라도 그 다음에 나오는 양수들로 인해 모두 누적시킨 합이 더 클 수도 있다.

현재 index 까지 도달하였을 때 최선의 sub array 누적 합을 acc 배열에 저장했다.

누적합이 이때까지의 최대합(sum)보다 큰 경우 sum을 업데이트 한다.

도중에 현재 index의 값 하나만으로도 이때까지 계산해온 누적합보다 이미 더 큰 경우가 생길 수 있다. 이런 경우엔 계산할 sub array를 여기서부터 새로 갱신한다.


```javascript
var maxSubArray = function(nums) {
    let sum = 0;

    const acc = [0];
    acc[0] = nums[0];
    sum = nums[0];

    for (let i = 1; i < nums.length; i++) {
        if (acc[i - 1] + nums[i] < nums[i]) { // new start
            if (nums[i] > sum) {
                sum = nums[i];
            }
            acc[i] = nums[i];
        } else if (acc[i - 1] + nums[i] > sum) {
            sum = acc[i - 1] + nums[i];
            acc[i] = acc[i - 1] + nums[i];
        } else {
            acc[i] = acc[i - 1] + nums[i];
        }
    }

    return sum;
};
```
