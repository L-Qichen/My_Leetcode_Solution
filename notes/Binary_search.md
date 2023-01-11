# 二分查找：
常用于已经排好序的数组，通过数组的最左值的 index（l=0）和最右值的 index（r=arr.length) 来获取数组的中间值。如果中间值不是目标值，则比较中间值和目标值的大小，并根据大小改变 l 或 r（缩减搜索区域）。因为每次都能将搜索区域减半，所以时间复杂度为O(logN)。

使用 binary search 时要注意两个基本原则：1. 每次缩减搜索区域；2. 每次缩减不能排除潜在答案。

### binary search 模版
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
            // int mid = (l + r) / 2;
            int mid = l + (r - l) / 2;
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
    * 缩减搜索空间：l = mid, r = mid - 1 **或者** l = mid + 1, r = mid（二选一，具体选哪个根据题目要求结合 binary search 的两个基本原则决定）;
3. 万用型（最接近3的数）
    * 循环条件：l < r - 1;**（l 和 r 相邻但不等于）**
    * 缩减搜索空间：l = mid, r = mid;

**关于 mid 的值**
有两种方式计算 mid：
1. (l + r) / 2;
2. l + (r - l) / 2;

两种方式的结果是一样的，但是 由于（l + r）可能出现加法溢出的情况，即加法的结果大于整型能够表示的范围，所以推荐在做题过程中使用第二种方法计算。因为 l 和 r 都是正数，因此（r - l）不会出现加法溢出问题。

### LeetCode 原题
* 33. Search in Rotated Sorted Array
```Java
public int search(int[] nums, int target) {
        // 检查数组是否为空
        if (nums == null || nums.length == 0) return -1;
        int l = 0, r = nums.length - 1;
        // 使用万用型模版
        while (l < r - 1) {
            int mid = l + (r - l) / 2;
            // 检查左边数组是否为有序数组
            if(nums[mid] >= nums[0]) {
                // 如果左半部分为有序数组，再检查target是否被包含在左侧数组内
                if(target >= nums[0] && target <= nums[mid]) {
                    // 如果左半数组有序且包含target，则截取左半数组并再搜索
                    r = mid;
                    // 如果左半数组有序但不包含target，则截取右半数组并再搜索
                } else {
                    l = mid;
                }
            } else { // 如果左半部分不是有序数组，则右半部分肯定为有序数组
                //逻辑同上一个条件判断，检查target是否包含在右侧有序数组内
                if (target >= nums[mid] && target <= nums[nums.length - 1]) {
                    l = mid;
                } else {
                    r = mid;
                }
            }
        }
        // 万用型模版最后跳出while循环时会留下两个元素
        //所以最后一步检查这两个元素是否有一个是target
        if(nums[l] == target) {return l;}
        if(nums[r] == target) {return r;}
        return -1;
    }
```
这道题的思路基本可以总结为先缩减搜索范围直到找到一个有序的部分，然后再从该有序的部分中找target。

