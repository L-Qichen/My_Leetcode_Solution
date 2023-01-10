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
上面的例子是 binary search 的基础题型，即在有序数组中搜索目标值并返回该目标值在数组中的 index。根据题目不同的要求，binary search 的模版在上列代码的基础上主要有三种变形：
1. 找一个准确值（上述的例子即是这种题型） 
    * 循环条件：l <= r; (等于，当数组只有一个元素时)
    * 缩减搜索空间：l = mid + 1, r = mid - 1;
2. 找一个模糊值（例：比3大的最小数，第一个比3大的数）
    * 循环条件：l < r;
    * 缩减搜索空间：l = mid, r = mid - 1 **或者** l = mid + 1, r = mid（二选一）;
3. 万用型（该模版同样可以用于替代前两个题型）
    * 循环条件：l < r - 1;
    * 缩减搜索空间：l = mid, r = mid;
