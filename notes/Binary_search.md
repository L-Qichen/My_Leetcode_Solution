#二分查找：
常用于已经排好序的数组，通过数组的最左值的 index（l=0）和最右值的 index（r=arr.length) 来获取数组的中间值。如果中间值不是目标值，则比较中间值和目标值的大小，并根据大小改变 l 或 r（缩减搜索区域）。因为每次都能将搜索区域减半，所以时间复杂度为O(logN)。

使用 binary search 时要注意两个基本原则：1. 每次缩减搜索区域；2. 每次缩减不能排除潜在答案。

###binary search 模版
常规应用：
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```
java:
```Java
public int binarySearch(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        while(l <= r){
            int mid = (l + r) / 2;
            if(nums[mid] == target) {
                return mid;
            } else if (nums[mid] > target) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return -1;
    }
```